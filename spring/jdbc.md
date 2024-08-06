# Spring JDBC

*Last Updated : 05/2024 - Spring 6.2 - Spring Boot 3.4.*

### Summary

- [Java Database Connectivity (JDBC)](#java-database-connectivity-jdbc)
- [JDBC Template](#jdbc-template)
    - [Basic syntax](#basic-syntax)
- [Callbacks](#callbacks)
- [Exceptions](#exceptions)

#
> Main sources : [Spring Academy Courses](https://spring.academy/home), [documentation](https://spring.io/projects/spring-framework).

<br>

## Java Database Connectivity (JDBC)

- Java **API** for database access and queries.

- Oriented towards **relational databases**.

<br>

*Ex :*

``` java
public List<User> findByLastName(String lastName) {
    List<User> userList = new ArrayList<>();

    String sql = "SELECT first_name, age, FROM USER WHERE last_name=?";

    try(
        Connection con = dataSource.getConnection();
        PreparedStatement ps = con.prepareStatement(sql)) {
        
        ps.setString(1, lastName);

        try(ResultSet rs = ps.executeQuery()) {
            while(rs.next()) {
                userList.add(new User(rs.getString("first_name")));
            }
        }

    } catch(SQLException sqle) {
        // ???
    }
}
```
**<u>Issues</u>** :

- Lot of **boilerplate** code to prepare, execute the query and handle exceptions.
- Prone to errors in **mapping** and **connection management**.
- Forced to handle `SQLExceptions` in place or through manual propagation.

<br>

## JDBC Template

- Uses the **template-method** design pattern ([related doc.](../java/design-patterns.md)).

- Defines outlines or skeleton of an algorithm and hide large amount of boilerplate code :

    - Connection aquisition.
    - Statement preprocessing.
    - Statement execution.
    - Result set processing.
    - Exceptions handling.
    - Connection release.

- *Initialization* :

    - Only requires a data source.
    - **Thread-safe**.
    - Syntax : `JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);`.

- Instantiated as field of a repository implementation class through the constructor, then used for queries.

#
### Basic syntax

- *Simple type single Object :*

``` java
int count = jdbcTemplate.queryForObject("SELECT COUNT(*) FROM CUSTOMER WHERE age > ?", Integer.class, age);
```
- Defines the return type to map the result to.
- `queryForObject` used for simple type return.
- Binds arguments to "?".

<br>

- *Multiple Objects :* `query`.

<br>

- *Single row as Object :* `queryForMap`.

    - Returns a `Map<column_name, column_value>`.

<br>

- *Multiple rows as Object :* `queryForList`.

    - Returns a list of maps for each row.
    - **Memory consuming**.

<br>

- *Create - Update - Delete - Insert :*

``` java
return jdbcTemplate.update(
    "INSERT INTO USER(first_name, last_name, age)" + "VALUES (?, ?, ?)", 
    user.getFirstName(),
    user.getLastName(),
    user.getAge());
```
- Returns the number of rows inserted.
- `update` used for everything.

<br>

- *Mapping to custom Object :*

    - Use of **callback** mappers.
    - May prefer to use an **ORM** instead (like **JPA**).
    - Useful for complex queries (joints...).

## Callbacks

- `RowMapper`

*Ex :*

``` java
List<Customer> result = jdbcTemplate.query(someSql,
    new RowMapper<Customer>() {
        public Customer mapRow(ResultSet rs, int row) throws SQLException {
            // ...
        }
    }
);
```
``` java
List<Customer> result = jdbcTemplate.query(someSql,
    (rs, rowNum) -> new Customer(rs.getString("name")) // Callback is iterated over rows in case of list.
);
```
<br>

- `ResultSetExtractor`

    - The result set needs to be parsed manually. 

*Ex :*

``` java
return jdbcTemplate.query(
    "SELECT ... FROM order o, item i ... confirmation_id = ?",
    (ResultSetExtractor<Order>) (rs) -> { // Cast needed.
        Order order = null;
        while(rs.next()) {
            if(order == null)
                order = new Order(rs.getLong("ID"), rs.getString("NAME"));
            order.addItem(mapItem(rs));
        }
        return order;
    }, number);
```
<br>

- `RowCallbackHandler`

    - Processes the entire result set to alternative destinations (file...) without returning anything.

<br>

## Exceptions

- Spring only throws runtime (**unchecked**) exceptions to avoid *tight-coupling* of checked exceptions.

- Traditional **JDBC** throws a checked `SQLException` for data access problems.

<br>

**<u>Issues</u>** :

- Too *general* - one exception for every database error.

- Disadvantages of checked exception :

    - Calling class knows about the access implementation (use of JDBC).
    - Forced to be handled in the method or passed through parent methods : **tight-coupling**.

<br>

**<u>Improvements</u>** :

- Spring provides an **unchecked** `DataAccessException` hierarchy :

    - `SQLException` **error codes** are mapped into meaningful exceptions.

- **Loose-coupling** : hides framework implementation.

- Consistent across all **supported** data access techologies.