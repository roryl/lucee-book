# Transactions
Lucee supports SQL transactions via the use of the `transaction {}` block. It is best practice to always use transactions with SQL  queries, even when not strictly necessary. Doing so ensures consistency with your database access. 

##Basic Transaction
This example shows the most basic transaction syntax. But since this is a SELECT statement, nothing is being modified. Technically a transaction provides no benefit here, but it is important to be in the habit of combining SQL statements into transactions.

<noscript>
```
<cfscript>
transaction {
	query name='employeeCount' {
		echo("SELECT count(*) FROM employees");
	}
}
writeDump(employeeCount);
</cfscript>
```
</noscript>

The dumb would result in:

![](basic_transaction.png)

##Transaction with Changes
