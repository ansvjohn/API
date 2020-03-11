<?php
if( isset($_POST['submit']) )
{ 
    //be sure to validate and clean your variables
    $val = htmlentities($_POST['val']);
    $val1 = htmlentities($_POST['val1']);
    $val2 = htmlentities($_POST['val2']); 
    //then you can use them in a PHP function. 
    $result = convertCurrency($val, $val1, $val2);
    echo $result;
    exit;
}
?>
<?php 
function convertCurrency($amount,$from_currency,$to_currency){
  $apikey = '940c76aa4755472e52b9';

  $from_Currency = urlencode($from_currency);
  $to_Currency = urlencode($to_currency);
  $query =  "{$from_Currency}_{$to_Currency}";

  // change to the free URL if you're using the free version
  $json = file_get_contents("https://free.currconv.com/api/v7/convert?q=INR_USD&compact=ultra&apiKey={$apikey}");
  $obj = json_decode($json, true);

  $val = floatval($obj["$query"]);


  $total = $val * $amount;
  return number_format($total, 2, '.', '');
} 
//uncomment to test
//echo convertCurrency(10, 'USD', 'INR');
?>
<form action="" method="POST">
    Amount: 
    <input type="text" name="val" id="val1"></input> 
    Inserisci number1: 
    <input type="text" name="val1" id="val1"></input> 

    <br></br>
    Inserisci number2:
    <input type="text" name="val2" id="val2"></input>

    <br></br>

    <input type="submit" name="submit" value="send"></input>
</form> 
