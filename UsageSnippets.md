

**At the beginning of a script always include proper initiation block**
## Initiation ##
```
//include particular file for entity you need (Client, Invoice, Category…)
include_once “library/FreshBooks/Client.php”;

//you API url and token obtained from freshbooks.com
$url = “your-url-please-replace”;
$token = “your-token-please-replace”;

//init singleton FreshBooks_HttpClient
FreshBooks_HttpClient::init($url,$token);
```

## Get Client Data ##
```
//new Client object
$client = new FreshBooks_Client();

//try to get client with client_id 3
if(!$client->get(3)){
    //no data – read error
    echo $client->lastError;
}
else{
    //investigate populated data
    print_r($client);
}
```

## New Client ##
```
//new Client object
$client = new FreshBooks_Client();

//populate client’s properties
$client->email = ‘test@test.com’;
$client->firstName = ‘Chad’;
$client->lastName = ‘Smith’;

//all other required properties should be populated

//try to create new client with provided data on FB server
if(!$client->create()){
    //read error
    echo $client->lastError;
}
else{
    //investigate populated data
    print_r($client);
}
```

## New Invoice ##
```
//new Invoice object
$invoice= new FreshBooks_Invoice();
//populate data
$invoice->clientId = 123;
$invoice->date = ‘2009-06-03′; //mysql format

//all other required properties should be populated

//lines (items) is array of asoc. arrays
$invoice->lines = array(
    //1st item
    array(
        ‘name’=>’xyz’,
        ‘unitCost’=>99.99,
        //all other required properties should be populated
    ),
    //2nd item
    array(
        ‘name’=>’yyy’,
        ‘unitCost’=>199.99,
    )
);

//try to create new invoice with provided data on FB server
if(!$invoice->create()){
    //read error
    echo $invoice->lastError;
}
else{
    //investigate populated data
    print_r($invoice);
}
```

## List/Search Projects ##
```
//create new Project object
$project = new FreshBooks_Project();

//listing function definition void   listing  ( &$rows,  &$resultInfo, [ $page = 1], [ $perPage = 25], [ $filters = array()])
//get projects, 25 per page, page 1, where project belong to client id 3
$project->listing($rows,$resultInfo,1,25,array('client_id'=>3));

//dump result data
print_r($rows);
print_r($resultInfo);
```