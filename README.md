# parsianPay
Easily integrate PHP application with parsian bank payment.

# Installation
``` bash
$ composer require mastercode724/parsian-ipg
```

# Example Usage
# Example For Pay

``` bash
use Mastercode724\ParsianIPG\ParsianIPG;
use Mastercode724\ParsianIPG\Entities\SalePaymentResult;

$parsianIPG=new ParsianIPG('scsdsdfbdsthsgfnfgndg');//set parsian pin
$OrderId = (float)(time() . rand(000,999)); // factor number
$Amount  = 1000; // amount to pay
$CallbackUrl='http://example.ir/callback' ; // set callback url
$additionalData='' ; // set Additional Data max 500 character
$originator='' ; // set Originator max 50 character
$isLog=true; //is log request and result
$addressLogger="";//is log file address request and result
$salePaymentResult=$parsianIPG->salePayment($OrderId,$Amount,$CallbackUrl,$additionalData,$originator,$isLog,$addressLogger);
if($parsianIPG->isReadyRedirect($salePaymentResult)){
    $parsianIPG->redirect($salePaymentResult);// redirect to parsian bank gateway  for payment  
}


 
```

# Example For Callback
``` bash
use Mastercode724\ParsianIPG\ParsianIPG;
use Mastercode724\ParsianIPG\Entities\ConfirmPaymentResult;
  
$parsianIPG=new ParsianIPG('scsdsdfbdsthsgfnfgndg');//set parsian pin 
$isLog=true; //is log request and result
$addressLogger="";//is log file address request and result
$confirmPaymentResult = $parsianIPG->confirmPayment($isLog,$addressLogger);
if($parsianIPG->isReadyConfirm($confirmPaymentResult)){
    die(' Payment OK '); 
}else{
    if($confirmPaymentResult instanceof ConfirmPaymentResult){ 
        echo $confirmPaymentResult->getMessage();
    }
} 





```


# Example For reverse
``` bash
use Mastercode724\ParsianIPG\ParsianIPG;
use Mastercode724\ParsianIPG\Entities\ReversalResult;

$parsianIPG=new ParsianIPG('scsdsdfbdsthsgfnfgndg');//set parsian pin 
$isLog=true; //is log request and result
$addressLogger="";//is log file address request and result
$reversalResult = $parsianIPG->reversal(12545485,$isLog,$addressLogger);//reverse token payment
if($parsianIPG->isReadyReversal($reversalResult)){
    die(' Reverse Payment OK '); 
}else{
    if($reversalResult instanceof ReversalResult){ 
        echo $reversalResult->getMessage();
    }
}



```
