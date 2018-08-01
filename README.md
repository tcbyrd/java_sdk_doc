# Fedex Cross Border SDK Java Project

## Summary
Built to evolve, with cutting edge web technology. This Java SDK uses REST API to connect to our backend, and it is fully integrated with our new Checkout API.
We rely on strong and accepted technology in the Internet Industry.

## Requirements

* Java - minimum version 7


## Installation

### Via Maven repository (coming soon...)
#### Maven
```xml
<dependency>
  <groupId>com.fcb</groupId>
  <artifactId>fedexcrossborder-sdk-java</artifactId>
  <version>1.0</version>
</dependency>
```
#### Gradle
```gradle
compile group: 'com.fcb', name: 'fedexcrossborder-sdk-java', version: '1.0'
```
#### SBT
```sbt
libraryDependencies += "com.fcb" % "fedexcrossborder-sdk-java" % "1.0"
```

### Manual
Download Jar file from ... and put it in your classpath.

#### Dependencies
* io.github.openfeign **feign-core** 9.5.0
* io.github.openfeign **feign-gson** 9.5.0
* io.github.openfeign **feign-slf4j** 9.5.1
* io.github.openfeign **feign-httpclient** 9.5.1
* commons-codec **commons-codec** 1.9
* org.slf4j **slf4j-api** 1.7.25


## Configuration options

In order to use the Java SDK you have three configuration options.

### Configuration file

**config.properties** file with REST API configuration properties. Here is an example, change the URLs accordingly:

```properties
com.fcb.checkout.service-url=http://checkout.ecommerce.bongo1.com
com.fcb.geo-location.service-url=http://checkout.ecommerce.bongo1.com
com.fcb.currency.service-url=http://checkout.ecommerce.bongo1.com
com.fcb.web-app.service-url=http://purplepay.stage1.bongo1.com
com.fcb.tracking.service-url=http://purplepay.stage1.bongo1.com
com.fcb.merchant-control.service-url=http://services.merchantdirect.bongo1.com
com.fcb.connect.service-url=https://api.crossborder.fedex.com/services/v45
com.fcb.distribution.service-url=https://services.crossborder.fedex.com
com.fcb.checkout.partner-key=
com.fcb.checkout.auth-token=
com.fcb.checkout.user=
com.fcb.checkout.password=
```
You can use only `com.fcb.checkout.auth-token` or the combination `com.fcb.checkout.user` and `com.fcb.checkout.password`.  

### System properties
If you don't want to define a **config.properties** file, you can define system variables with the same names and values. 

#### JBoss example (**standalone.xml**):

```xml
<system-properties>
  <property name="com.fcb.checkout.service-url" value="http://checkout.ecommerce.bongo1.com"/>
  ...
</system-properties>
```
#### WebLogic example (**weblogic.properties**):
```properties
com.fcb.checkout.service-url=http://checkout.ecommerce.bongo1.com
...
```
#### Some others
```
... -Dcom.fcb.checkout.service-url=http://checkout.ecommerce.bongo1.com ...
```

### None
You can also use the SDK without any additional configuration by just using the constructors that receive the needed data as parameters. See [Main Classes](#main-classes)

## Getting Started

This SDK includes two options to integrate, the first is through the Java API and second through the HTML Widget using the Java API.
The API is contained in **fedexcrossborder-sdk-java.jar** which includes the packages with all the classes, the main package is `com.fcb.sdkjava.api` where API Classes are contained. 
The next contains the Java API:

To integrate with this API it's necessary to instance some of the API Classes depending on what your needs are.
Each API contains different methods and each one contains logic, parameters and return types corresponding to the domain objects (package `com.fcb.sdkjava.domain`)

### Main Classes

* `CheckoutAPI` 
Is a component to expose the methods of Checkout REST API, this class has three different constructors depending on how the configuration parameters will be passed

  * `CheckoutAPI(String url, String partnerKey, String authToken)` : this receives the URL, partner key and an authToken which consists of an encode base64 string of user and password.
  * `CheckoutAPI(String url, String partnerKey, String user, String password)` : this receives string texts of the URL, partner key, user and password.
  * `CheckoutAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `WidgetAPI` 
Is a component that contains two getWidget methods which returns HTML content, this class has two different constructors depending on how the configuration parameters will be passed

  * `WidgetAPI(String url)` : this receives the URL string of the API server.
  * `WidgetAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `TrackingAPI` 
Is a component that contains features to monitoring an order, this class has two different constructors depending on how the configuration parameters will be passed

  * `TrackingAPI(String url)` : this receives the URL string of the API server.
  * `TrackingAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `CurrencyAPI` 
Is a component with the features to calculate exchange rates, this class has two different constructors depending on how the configuration parameters will be passed

  * `CurrencyAPI(String url, String partnerKey, String authToken)` : this receives URL string , partner key and an authToken of the API server.
  * `CurrencyAPI(String url, String partnerKey, String user, String password)` : this receives string texts of URL, partner key, user and password.
  * `CurrencyAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `GeoLocationAPI` 
Is a component with location features, this class has two different constructors depending on how the configuration parameters will be passed.

  * `GeoLocationAPI(String url)` : this receives the URL string of the API server.
  * `GeoLocationAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `MerchantControlAPI`
This is a component with the merchant control utilities, this class has three different constructors depending on how the configuration parameters will be passed.

  * `MerchantControlAPI(String url, String partnerKey, String authToken)` : this receives the URL, partner key and an authToken which consists of an encode base64 string of user and password.
  * `MerchantControlAPI(String url)` : this receives URL string of the API server.
  * `MerchantControlAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `ConnectAPI`
This component provides access to the FedEx Cross Border Connect services through Java components, this class has two different constructors depending on how the configuration parameters will be passed, and was generated with version v45 of the Connect API WebService then if the version changes it is necessary to change the names in order the WSClient and works well.

  * `ConnectAPI(String url, QName serviceQName, QName portQName)` : this receives the URL of the WSDL, and the QName for service and port.
  * `ConnectAPI(String url)` : this receives the URL of the WSDL for the ConnectAPI, in this case serviceQName and portQName are by default (BongoServiceV45Service and BongoServiceV45Port).
  * `ConnectAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties and in this case serviceQName and portQName are by default (BongoServiceV45Service and BongoServiceV45Port).

* `DistributionAPI`
This is a component from the Marketer functionalities group and it contains the methods related with the distribution process, this class has three different constructors depending on how the configuration parameters will be passed and provides the access to the REST Distribution Services.

  * `DistributionAPI(String url, String partnerKey, String authToken)` : this receives the URL, partner key and an authToken which consists of an encode base64 string of user and password.
  * `DistributionAPI(String url)` : this receives URL string of the API server.
  * `DistributionAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.

* `CustomAPI`
This is a component from the Marketer functionalities group and it contains the methods related with the ordering process, this class has three different constructors depending on how the configuration parameters will be passed and provides the access to the REST Custom Ordering Services.

  * `CustomAPI(String url, String partnerKey, String authToken)` : this receives the URL, partner key and an authToken which consists of an encode base64 string of user and password.
  * `CustomAPI(String url)` : this receives URL string of the API server.
  * `CustomAPI()` : this takes the configuration parameters from the **config.properties** file or from the system properties.


### Methods
* `CheckoutAPI` 
Below are the methods included in this API. If you need more detail about how consuming these methods are, you can review the corresponding integration test class **CheckoutIT**

  * `getAvailableShippingMethods(String checkoutId)`: this gets all available shipping methods in a created checkout instance.
  * `availablePaymentMethods(String checkoutId)`: this gets all available payment methods in a created checkout instance.
  * `getAvailableCountries()`: this gets all available countries configured by partner.
  * `getAvailableLanguages()`: this gets all available languages configured by partner.
  * `updateCustomerAttributes(String checkoutId, CustomerAttributes attributes)`: this updates the custom attributes in a created checkout instance.
  * `updateBillingAddress(String checkoutId, Address billingAddress)`: this updates  the customer billing address in a created checkout instance.
  * `updateShippingAddress(String checkoutId, Address shippingAddress`: this updates  the customer shipping address in a created checkout instance.
  * `updateShippingMethod(String checkoutId, ShippingMethodOption shippingMethodOption`: this updates  the customer shipping address in a created checkout instance.
  * `createCheckout(Cart cart)`: this creates a Checkout using a predefined cart object.
  * `getCheckout(String checkoutId)`: this gets the Checkout instance from an id.
  * `patchCheckout(String checkoutId, Cart cart)`: this updates the Checkout instance from an id sending a cart.
  * `pay(String checkoutId, PaymentInfo paymentInfo)`: Proceed to pay a created checkout instance.
  * `addItem(String checkoutId, Product product)`: this adds a new product to a created checkout instance.
  * `updateItem(String checkoutId, Product product)`: this updates  a created product in a created checkout instance.
  * `deleteItem(String checkoutId, Product product)`: this deletes a created product in a created checkout instance.
  * `setShippingMethod(String checkoutId, int code)`: this sets the shipping method to an order with the CheckouId and the code of the shipping method.

* `WidgetAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **WebAppIT**

  * `getWebAppWidget(Cart cart)`: this gets purplepay widget using a defined cart object.
  * `getMonitoringWidget(WidgetRequest request`: this gets map widget using a the mechant info.

* `TrackingAPI` 
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **TrackingIT**

  * `getOrders(String email)`: this gets customer orders by email.
  * `getOrderActivities(String orderId)`: this gets order activities by Id.
  * `getBoxItems(String trackingNumber)`: this gets item of a given tracking id.

* `CurrencyAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **CurrencyIT**

  * `getExchangeRate(List<String> from, List<String> to)`: this gets exchange rate for every given currency, each currency should be sent in currency abbreviation form, example "USD".

* `GeoLocationAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **GeoLocationIT**

  * `getCountry(String ip)`: this returns the country of a given IP address.

* `MerchantControlAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **MerchantControlIT**

  * `saveCarrierCredentials(CarrierCredentials credentials)`: this allows the carrier credentials to be saved and returns the token of the saved carrier.
  * `packNotification(PackNotification packNotification)`: this notifies a package and returns the id of the pack notified and documents URLs.
  * `makeItemRefund(ItemRefund itemRefund)`: this returns a true in isSuccess attribute if the item was refunded or otherwise false.
  * `cancelPackNotification(int idPackNotification)`: this returns a true in isSuccess attribute if the pack notification was successful canceled or otherwise false.
  * `getDocuments(int idPackNotification)`: this returns an array with the documents' information including the document URL .
  * `makeCustomRefund(CustomRefund customRefund)`: this returns a true in isSuccess attribute if the refund was successful or otherwise false plus a response message.
  * `getReferences()`: this returns the carrier service categories with its specific carriers.

* `ConnecttAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **ConnectIT**

  * `connectSkuStatus(ConnectSkuStatusRequest request)`: this returns SKU and product status with the Product ID.
  * `connectProductInfo(ConnectProductInfoRequest request)`: this syncs the product database with FedEx Cross Border and returns the result of the operation with error = 0 if the process was successful.
  * `connectLandedCost(ConnectLandedCostRequest request)`: this calculates the total cost (duties, taxes and shipping costs) of a shipment to a specific country and returns the result.
  * `connectOrder(ConnectOrderRequest request)`: this allows the order detail to be sent and returns the result of the operation with error = 0 plus the tracking link if the process was successful.
  * `connectOrderTrackingUpdate(ConnectOrderTrackingUpdateRequest request)`: this allows the tracking numbers to update and/or add to any item for a submitted order. Returns the result of the operation with error = 0 plus the tracking link if the process was successful.
  * `connectOrderRemove(ConnectOrderRemoveRequest request)`: this method removes an existing order made with the connectOrder method and returns the result of the process.

* `DistributionAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **DistributionIT**

  * `router(RouterRequest request)`: this creates a shipment end-to-end and returns a domestic FedEx Label and up to three USPS international labels
  * `fedexGetLabel(FedexLabelRequest request)`: this creates a domestic shipment using the FedEx Express Saver service type, and returns the corresponding label, or an error message.
  * `checkEligibility(USPSRequest request)`: this checks if a given shipment is valid and returns a true if the process was successful.
  * `getLabelWithPackageInfo(USPSRequest request)`: this checks if a given shipment is valid and at the same time gets the corresponding label and returns a true if the process was successful.
  * `getLabelWithPackageID(String packageID)`: this checks if a given shipment is valid and at the same time gets the corresponding label and returns a true if the process was successful.

* `CustomAPI`
Below are the methods included in this API, if you need more detail about how consuming these methods are, you can review the corresponding integration test class **CustomIT**

  * `getAllOrders()`: this gets all the orders including its items without any params.
  * `getOrderByNumber(String orderId))`: this gets an order including its items by the order ID, and returns the corresponding label, or an error message.
  * `createOrder(Order order)`: this creates a new order and returns a true if the process was successful, the attribute orderNumber should not be filled in the request.
  * `updateOrder(String orderId, Order order)`: this checks if a given shipment is valid and at the same time gets the corresponding label and returns a true if the process was successful.
  * `cancelOrder(String orderId)`: this updates an existing order with the order number and the order object, and returns a true if the process was successful.
  * `rpsValidation(RPSShipmentInfo shipmentInfo)`: this calidates RPS with the shipment information in the FXCB system and returns a true if the process was successful.


### Samples 

For using the following examples, it's necessary to add the imports below:

```java
import com.fcb.sdkjava.api.*;
import com.fcb.sdkjava.domain.checkout.*;
import com.fcb.sdkjava.domain.currency.*;
import com.fcb.sdkjava.domain.geolocation.*;
import com.fcb.sdkjava.domain.tracking.*;
import com.fcb.sdkjava.domain.widget.*;
```

#### CheckoutAPI

##### Creating a Cart Object

Some methods of CheckoutAPI require a Cart Object in the following lines is showed how to create that object:

```java
//Merchant config
Merchant merchant = new Merchant();
merchant.setPartnerKey("7625511ed3383939386558db5e52c27b");
merchant.setLang("en");
merchant.setAutoOpen(true);
merchant.setEnablePinpoint(false);
merchant.setJoinDutyShipping(false);
merchant.setChangeNumberItems(true);
merchant.setMerchantControl(false);

//Order
Order order = new Order();
order.setDomesticShippingCharge(0);
order.setOrderCurrency("PEN");
order.setOrderTransit(3);
order.setCustomOrder_1("CUSTOM_ORDER_1");
order.setCustomOrder_2("CUSTOM_ORDER_2");
order.setCustomOrder_3("CUSTOM_ORDER_3");

//Address
Address address = new Address();
address.setFirstName("Juan Carlos");
address.setLastName("Ludeña");
address.setEmail("jludena@idigital.pe");
address.setPhone("2345678");
address.setAddress1("loas alphes");
address.setAddress2("loas alphes_2");
address.setCity("New York");
address.setCountry("PE");
address.setState("Alaska");
address.setZip("99812");
address.setCompany("otra");

//Customer
Customer customer = new Customer();
customer.setBilling(address);
customer.setShipping(address);

//Product
Product product = new Product();
product.setId("PRTEST-POMPOM-0001");
product.setName("48 PVC Boat Guides - Tie Down Engineerin");
product.setQuantity(1);
product.setUnitPrice(2.95);
product.setShipping(0);
product.setTotalPrice(2.95);
product.setRetailPrice(2.95);
product.setImage("");
product.setDescription("");
product.setCountryOfOrigin("PE");
product.setDistributionCountry("US");
product.setDistributionZip("");
product.setCustom_1("");
product.setCustom_2("");
product.setCustom_3("");
product.setSw("more");
product.setIndice(1);

//Cart creation
Cart cart = new Cart();
cart.setProducts(new Product[]{product});
cart.setMerchant(merchant);
cart.setOrder(order);
cart.setCustomer(customer);
cart.setShippingMethods(null);
```

##### Consuming `pay` service

Some methods of CheckoutAPI require a Pay Object in the following lines is showed how to create that object:

```java
PaymentInfo paymentInfo = new PaymentInfo();
paymentInfo.setPayType("creditcard");
paymentInfo.setCode("MASTERCARD");
paymentInfo.setCardNumber("5425233430109903");
paymentInfo.setCardExpMonth("4");
paymentInfo.setCardExpYear("2018");
paymentInfo.setCardCCV("411");

PaymentResponse paymentResponse = 
  new CheckoutAPI().pay(checkoutId, paymentInfo);
```

#### CurrencyAPI

##### Consuming `getExchangeRate` service

````java
List<String> from = Arrays.asList("PEN", "USD", "COP");
List<String> to = Arrays.asList("PEN", "AED", "COP", "BTC");

ExchangeRate result = new CurrencyAPI().getExchangeRate(from, to);
````

#### GeoLocationAPI

##### Consuming `getCountry` service

```java
GeoLocation result = new GeoLocationAPI().getCountry("8.8.8.8");
```

#### TrackingAPI

##### Consuming `getOrders` service
```java
String mail = "user_name@domain.com";
final List<CustomerOrder> orders = new TrackingAPI().getOrders(mail);
```

#### WidgetAPI

If you are going to do the integration through Widget contents, the following lines show you how to do that. The following are just examples using JSP and Servlets that should be changed according your technology stack.

##### Add the WebApp Widget to HTML

To include the widget in a web page it's necessary to call the API from a component that can set the widget content into the response. That component can be a Controller, for example:

This is an example of a call code from a controller. Notice that the method uses a `Cart` as parameter, see [Creating cart object](#creating-a-cart-object) to build it.

```java
 String result;
 try {
    result = new WidgetAPI(URL).getWebAppWidget(buildCart());
 } catch (FedexCrossBorderException e) {
    result = "Failed: " + e.getMessage();
 }
 req.setAttribute("widget", result);
 ```

And the call from the web page

```html
 <div id="widget-fcb-button-container">
   <%= request.getAttribute("widget") %>
 </div>
 <button type="button" class="btn btn-success fcb_web_app">
   Proceed to Secure Checkout
 </button>
```

##### Add the Monitoring Widget to HTML

To include the widget in a web page it's necessary to call the API from a component that can set the widget content into the response. That component can be a Controller, for example:

This is an example of a call code from a controller

```java
String partnerKey ="PARTNER_KEY";
String email = "username@domain.com";

WidgetRequest request = new WidgetRequest();
request.setCustomerInfo(new CustomerInfo());
request.setMerchantCredential(new MerchantCredential());

request.getCustomerInfo().setEmail(email);
request.getMerchantCredential().setPartnerKey(partnerKey);

String result;
try {
  result = new WidgetAPI(URL).getMonitoringWidget(request);
} catch (FedexCrossBorderException e) {
  result = "Failed: " + e.getMessage();
}

req.setAttribute("widget", result);
```

And the call from the web page

```html
<button type="button" class="btn btn-success monitoring_web_app">
  Proceed to Monitoring
</button>

<div id="widget-fcb-button-container" >
  <%= request.getAttribute("widget") %>
</div>
```
#### MerchantControlAPI

##### Consuming `packNotification` service

In order to call the PackNotification service it is first necessary to create an order calling the `createCheckout` method of the CheckoutAPI with the flag `MechantControl` in **true** like the one below:
```java
Cart cart = new Cart();

        Address address = new Address();
        address.setFirstName("John");
        address.setLastName("Doe");
        address.setCompany("My Biz");
        address.setAddress_1("10-123 1/2 MAIN STREET NW");
        address.setAddress_2("MONTREAL QC H3Z 2Y7");
        address.setCity("Montreal");
        address.setCountry("CA");
        address.setState("Quebec");
        address.setZip("H3Z 2Y7");
        address.setPhone("1-514-888-9999");
        address.setEmail("john.doe@mybiz.com");
        address.setCustom_1("Custom Value 1");
        address.setCustom_2("Custom Value 2");
        address.setCustom_3("Custom Value 3");
        address.setTaxId("123456789");

        cart.setBillingAddress(address);
        cart.setShippingAddress(address);

        ShippingMethodOption method = new ShippingMethodOption();
        method.setCode(ShippingMethodOption.INTERNATIONAL_STANDARD);
        cart.setShippingMethod(method);


        MerchantShippingMethod merchantShippingMethod = new MerchantShippingMethod();
        merchantShippingMethod.setCode("0");
        merchantShippingMethod.setName("Intl Priority");
        merchantShippingMethod.setTransitTime(8);
        merchantShippingMethod.setDutiableTransitCost("200");
        merchantShippingMethod.setChargedTransitCost("125");
        merchantShippingMethod.setChargedTransitCostMessage("10 Discount Message");
        merchantShippingMethod.setSortIndex(0);
        merchantShippingMethod.setServiceLevelCategory(2);

        MerchantShippingMethod merchantShippingMethod2 = new MerchantShippingMethod();
        merchantShippingMethod.setCode("1");
        merchantShippingMethod.setName("Intl Economy");
        merchantShippingMethod.setTransitTime(11);
        merchantShippingMethod.setDutiableTransitCost("105");
        merchantShippingMethod.setChargedTransitCostMessage("20 Discount Message");
        merchantShippingMethod.setSortIndex(1);
        merchantShippingMethod.setServiceLevelCategory(1);

        MerchantShippingMethod merchantShippingMethod3 = new MerchantShippingMethod();
        merchantShippingMethod.setCode("2");
        merchantShippingMethod.setName("Intl Economy Freight");
        merchantShippingMethod.setTransitTime(15);
        merchantShippingMethod.setDutiableTransitCost("80");
        merchantShippingMethod.setChargedTransitCost("55");
        merchantShippingMethod.setChargedTransitCostMessage("30 Discount Message");
        merchantShippingMethod.setSortIndex(2);
        merchantShippingMethod.setServiceLevelCategory(1);

        MerchantShippingMethod merchantShippingMethods[] = {merchantShippingMethod, merchantShippingMethod2, merchantShippingMethod3};
        cart.setMerchantShippingMethods(merchantShippingMethods);

        Product product = new Product();
        product.setId("FXB-demoWebapp-1");
        product.setName("576 #2 Pencils");
        product.setPrice("37.25");
        product.setRetailPrice(37.25);
        product.setQuantity(100);
        product.setShipping(0.00);
        product.setCustom_1("");
        product.setCustom_2("");
        product.setCustom_3("");
        product.setDistributionCountry("US");
        product.setCountryOfOrigin("US");
        product.setDistributionZip("");
        product.setProductTransit("3");

        Product product2 = new Product();
        product2.setId("FXB-demoWebapp-2");
        product2.setName("576 #3 Pencils");
        product2.setPrice("37.25");
        product2.setRetailPrice(37.25);
        product2.setQuantity(100);
        product2.setShipping(0.00);
        product2.setCustom_1("");
        product2.setCustom_2("");
        product2.setCustom_3("");
        product2.setDistributionCountry("US");
        product2.setCountryOfOrigin("US");
        product2.setDistributionZip("");
        product2.setProductTransit("3");

        Product productArray[] = {product, product2};
        cart.setProducts(productArray);

        cart.setOrderTransit(3);
        cart.setCustomOrder_1("Custom Value 1");
        cart.setCustomOrder_2("Custom Value 2");
        cart.setCustomOrder_3("Custom Value 3");
        cart.setDomesticShippingCharge("0.00");
        cart.setMerchantCurrency("USD");
        cart.setChargeDutyTax(true);
        cart.setChargeLossDamageProtection(true);
        cart.setRetailerOrderNumber("A-1234-001");

        MerchantAttributes merchantAttributes = new MerchantAttributes();
        merchantAttributes.setConfirmationUri("");
        merchantAttributes.setMechantControl(true);
        cart.setMerchantAttributes(merchantAttributes);

        CustomerAttributes attributes = new CustomerAttributes();
        attributes.setIp("127.0.0.1");
        attributes.setTimezone("America/Montreal");
        attributes.setLocale("en_US");
        cart.setCustomerAttributes(attributes);

        Checkout checkout = checkoutApiMD.createCheckout(cart);
```

Then the order must be paid through the `pay` method of the CheckoutAPI with the checkoutId answered by createCheckout method and then the order has to be processed in Fedex's systems to be able to notify.
As in bellow the example of calling payment method.

```java
        PaymentInfo paymentInfo = new PaymentInfo();
        paymentInfo.setPayType("creditcard");
        paymentInfo.setCode("MASTERCARD");
        paymentInfo.setCardNumber("5425233430109903");
        paymentInfo.setCardExpMonth("4");
        paymentInfo.setCardExpYear("2018");
        paymentInfo.setCardCCV("411");

        PaymentResponse paymentResponse = api.pay(checkoutIdAnswered, paymentInfo);
```

Finally, at this point the `packNotification` method can be called, an example of a PackNotification Object for an order with number "1000374355" is given below,
taking into account that the CarrierToken is the code answered by the `saveCarrierCredentials` method.  (More examples in `MerchantControlIT.java`)

```java
    PackNotification packNotification = new PackNotification();
    packNotification.setCarrierToken("202e8b540d681837836db38ecf6b909e");
    packNotification.setFxcbOrderNumber("1000374355");
    packNotification.setTransitMethodCode("FDX-IE");
    packNotification.setReturnConfiguration("FDX-IE");
    packNotification.setInsure(true);
    packNotification.setInsureAmount("1.0");
    packNotification.setQtyBoxes(1);
    packNotification.setCallBackUrl("Merchant Call back URL for Notifications");

    Address addressPickup = new Address();
    addressPickup.setCompanyName("Konta");
    addressPickup.setAddress1("6 ave");
    addressPickup.setAddress2("");
    addressPickup.setCity("ardmore");
    addressPickup.setState("alberta");
    addressPickup.setZipCode("T0A 0B0");
    addressPickup.setCountry("CA");
    addressPickup.setPhone("131313123");
    addressPickup.setTaxId("");

    Address addressCompany = new Address();
    addressCompany.setCompanyName("Konta");
    addressCompany.setAddress1("6 ave");
    addressCompany.setAddress2("");
    addressCompany.setCity("ardmore");
    addressCompany.setState("alberta");
    addressCompany.setZipCode("T0A 0B0");
    addressCompany.setCountry("CA");
    addressCompany.setPhone("131313123");
    addressCompany.setTaxId("as12313");

    packNotification.setPickupAddress(addressPickup);
    packNotification.setConsignorAddress(addressCompany);

    Item item = new Item();
    item.setSku("FXB-demoWebapp-1");
    item.setCoo("CH");

    Box box = new Box();
    box.setBoxDimUom("CM");
    box.setBoxWeight(5);
    box.setBoxWeightUom("KG");
    box.setBoxLength(15);
    box.setBoxWidth(15);
    box.setBoxHeight(10);

    box.setItems(new Item[]{item});

    packNotification.setBoxesInfo(new Box[]{box});
    packNotification.setLabelFormat("PNG");
```

#### CustomAPI

##### Consuming `createOrder` service

To create a new order in the FXCB system it necessary to call the createOrder method passing an Order object with all the information as in the example bellow:
```java
    Order order = new Order();
    order.setName("My order 1");
    order.setShippingCost(98.2);
    order.setTotal(100.67);
    order.setWeight(72.3);
    order.setInsurance(1);
    order.setDuty(10);
    order.setTax(14);
    order.setDutyTaxType("DDU");
    order.setOrigin_country("PE");
    order.setInsuranceValue(50);
    order.setCurrency("PEN");
    order.setServiceMethod("Express");

    ShipmentInfo shipInfo = new ShipmentInfo();
    shipInfo.setFirstname("Andrea");
    shipInfo.setLastname("Camacho");
    shipInfo.setPhone("987655432");
    shipInfo.setEmail("testing@fcb.com");
    shipInfo.setCompanyName("Fedex Crossborder latam");
    shipInfo.setMainAddress("Avenida 111");
    shipInfo.setSecondAddress("Casa 222");
    shipInfo.setCity("Bogota");
    shipInfo.setState(" ");
    shipInfo.setZip("101011");
    shipInfo.setCountry("CO");
    order.setShipmentInformation(shipInfo);

    Item item = new Item();
    item.setName("");
    item.setDescription("");
    item.setQuantity(1);
    item.setPrice(25);
    item.setWeight(50);
    item.setImage("http://mipagina.com/mi_imagen2.jpg");
    item.setLength(10);
    item.setWidth(8);
    item.setHeight(7);
    item.setDimension(15);
    item.setProductId("ABC-123");
    item.setCountryOfOrigin("CO");
    Item itemArray[] = {item};
    order.setItems(itemArray);

    OrderResponse response = customApi.createOrder(order);
```


### Test 

The SDK includes test classes for all the API methods, those test classes are in the folder `test` in the package `com.fcb.sdkjava.api` and you can execute the test cases with the JUnit library or you can also use the SBT command `sbt test` or running these tests from an IDE like IntelliJ doing click on the test Class and then run.
