# Mid-Term-2_Exam_MongoDB_Bhanu_Kiran
Exam Answers
# Mid-Term-2_Exam_MongoDB_Bhanu_Kiran
Exam Answers
#Scenario A2 
#task1
create database collegeDb ;
create collection "students" ;
use collegeDB;
collegeDB.students.insertOne([
    {
        _id:101,
        "name":"Arun",
        "dept":"CSE",
        "marks": 78,
        "DBMS":85,
        "Maths":70
    }
])

#task2
collegeDB.students.insertOne([
    {
        _id:101,
        "name":"Rupa",
        "dept":"EC",
        "marks": 78,
        "DBMS":85,
        "Maths":99
    }
])
The error says that we cannot insert another entry with another the same _id value as duplicate id's are not allowed .
Here we cannot add a duplicate key i.e. _id to the document hence we get the error E11000 collegeDB.students index : _id_ dup key: { _id: 101}
#Task 3
collegeDB.students.insertOne([
    {
        _id:102,
        "name":"Bala",
        "dept":"IT",
        "marks": 66,
        "DBMS":60,
        "Maths":72
 , {
        _id:103,
        "name":"Chitra",
        "dept":"CSE",
        "marks": 91,
        "DBMS":95,
        "Maths":87
    }
,
        _id:104,
        "name":"Divya",
        "dept":"ECE",
        "marks": 72,
        "DBMS":55,
        "Maths":89
    }
,  {
        _id:105,
        "name":"Eswar",
        "dept":"IT",
        "marks": 84,
        "DBMS":88,
        "Maths":80
    }
, {
        _id:106,
        "name":"Farah",
        "dept":"CSE",
        "marks": 59,
        "DBMS":45,
        "Maths":73
    }
])

#Task 4

collegeDB.students.find(
    "dept":"CSE"
)

#Task 5

collegeDB.students.aggregate(
    $group{$avg{ $gte:{ "marks":75}
    }
    }
)


#Task 6

collegeDB.students.find(
   $in:["CSE","IT"]
)

#Task 7


collegeDB.students.aggregate(
    $elemMatch( $gt:( "DBMS":80))
)



#Task 8

collegeDB.students.find(
    $sort{"name":1,
  "marks":1,
  _id:0}

  
  
)



#Scenario A4 
#bankDB
replication is the process of creating sevelar duplicate secondary servers for the Primary server , incase the primary server crashes or if there is any failure , 
then the primary server can become the secndary server and the primary  server can become the secondary server .

The secondary servers communicate  with each other using "Heartbeat" and We may al;so make use of an arbiter in case we  don't have the budget for a secondary server 


 The redundancy which we create ensures that  the system is fault tolerant and incase of any failures or crashes the there is no loss , all the serveers have the same data.
 Replication is used because 
 a) It provides data redundancy  which is required for ensurinfg no  loss even is case of failure, the same data is kept on all the servers ( primary and secondary both 0 , it gives high availability even when the system/server crashes ) 
 b) It makes the system fault tolerant and resistant to data losses(protects against data losses).
 and the option to spraed read load to secondaries., there is always  exactly one primary server but there can be many secondary servers which may become rimary in case of failure through the process of election , where the server nay vote for itself or  the primary server may vote for it ( i.e. for the secondary server tkeing the place of the primary server .)


#Task 1 
 mongod --rs0/27017

 mongod --rs0/27018

 mongod --rs0/27019
 

 rs.initiate;

 Here mongod is the command which we will use for starting the servers and then later we will duplicate the data on them which is thert on the primary server . 

 # Task 2 
 the result returned is -> 
 [{name:'localost:27017', state:'PRIMARY', health: 1 },
 {name:'localost:27018', state:'SECONDARY', health: 1 },{name:'localost:27019', state:SECONDARY, health: 1 }
 ]


from this result we can see that the primary server is the server which is running on the localhsost 27017
  # task 3  
  bankDb.accounts.insertOne(
    "accNo": 1002, 
    "holder":Vimal",
    "balance":20000
    w:"majority"
  )

  # Task 4 

bankDb.accounts.secondaryPreferred()
We have to read the colletion named accounts in the bank DB using  secondaryPreferred
# Task 5  
the oplog created is -> 
{
    op:'i',
    ns:'bankDB.accounts',
    o:{_id:objectId('...'),accNo : 1001, holder: 'kumar', balance:5000},
    ts: Timestamp({t: <seconds>, i:1 }),
    ... and so on 
} -> from this oplog we can infer that the database is of a Bak and the DB is named bankDB , since bank servers require higher fault tolerance so that's why we would use replication for it . 
and the details of an account holder by the name -> "kumar" ,  with   the Balance  : 5000 

# Task 6
 The new primary is created by the process of election where the primary sever crashes and then one of the secondary server's becomes the sprimary server by the process of election where a secondary server may vote for itself or the primary server which is steppn down may give it one vote . 



# task 7 
rs.status()
replication ensures that all the servers have the sme data shared with them to ensure redundancy to prevent against failure. 



//repo lin -> https://literate-fishstick-v66r5qx44g4p2p4qv.github.dev/
