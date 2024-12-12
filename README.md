[desktopapp](https://github.com/karatelabs/karate/blob/master/karate-robot/src/test/java/robot/core/wordpad.feature)
[example](https://github.com/karatelabs/karate-examples)


Feature: Employee Database Operations

  Background:
    * url 'jdbc:mysql://localhost:3306/testdb'
    * def dbHelper = Java.type('common.helper.DatabaseHelper')
    * def dataHelper = new dbHelper('test')

  Scenario: Retrieve all employees in the HR department
    * def hrEmployees = dataHelper.executeQuery("SELECT * FROM employees WHERE department = 'HR'")
    * print hrEmployees
    * match hrEmployees[*].department contains 'HR'

  Scenario: Update salary of employees in Engineering department by increasing it by 10%
    * def updateQuery = "UPDATE employees SET salary = salary * 1.1 WHERE department = 'Engineering'"
    * def result = dataHelper.executeUpdate(updateQuery)
    * print result
    * match result == true

  Scenario: Delete an employee whose email is 'bob.johnson@example.com'
    * def deleteQuery = "DELETE FROM employees WHERE email = 'bob.johnson@example.com'"
    * def result = dataHelper.executeUpdate(deleteQuery)
    * print result
    * match result == true

  Scenario: Count the total number of employees
    * def totalEmployees = dataHelper.executeQuery("SELECT COUNT(*) AS total_employees FROM employees")
    * print totalEmployees[0].total_employees
    * match totalEmployees[0].total_employees > 0
