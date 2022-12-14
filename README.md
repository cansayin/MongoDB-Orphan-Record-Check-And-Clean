# MongoDB-Orphan-Record-Check-And-Clean
Command for check orphan record on mongodb and clean


#linkedin : https://www.linkedin.com/in/can-sayın-b332a157/
#cansayin.com

First run the following command
<pre id="example"><code class="language-lang"  style="color: #333; background: #f8f8f8;"> 
db.orderItems.find( { }, { _id: 1, _id: 0 } ).hint( { _id: 1 } ).explain(true)
</code></pre>

If output is grater than 0 that means there are orphan record
<pre id="example"><code class="language-lang"  style="color: #333; background: #f8f8f8;"> 
"chunkSkips" : 0,
</code></pre>
 
To clear orphan record run the following commands
<pre id="example"><code class="language-lang"  style="color: #333; background: #f8f8f8;"> 
var dbName: db.getName();
db.getCollectionNames().forEach(function(cName) {
  
    var nameSpace = dbName.concat("."+cName);
    result = db.runCommand({
      cleanupOrphaned: nameSpace
    });
    if (result.ok != 1)
      print(nameSpace + ":Unable to complete at this time: failure or timeout.")
   
  });
</code></pre>
