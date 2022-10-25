### What is a db transaction:
<ol>
<li>A single unit of work</li>
<li>Often made up of multiple db operations</li>
</ol>

<b>Example </b> :
Transfer 10USD from bank account 1 to bank account 2
<ol>
<li>Create a transfer record with amount = 10</li>
<li>Create an account entry for account 1  with amount = -10</li>
<li>Create an account entry for account 1  with amount = 10 </li>
<li>Subtract 10 from balance of account 1</li>
<li>Add 10 from balance of account 2</li>
</ol>

### WHy do we need dbtx
<ol>
<li>Provide a reliable and consistent uni of work, event in case system failure</li>
<li>Provide isolation between programs that access the database concurrently</li>
</ol>

