# Food-Delivery-LLD

Food Delivery Solution for Coderbyte


## Requirements

 A food delivery system requires the interaction of the restaurants, customers and delivery partners with the admin.
 
 
> Restaurants can register themselves.

> Users can create, update, delete, get their profiles.

> User can search for the restaurant using a restaurant name, city name.

> Restaurants can add, update the food menu.

> User can see the food menu. User can get the food items based on Meal type or Cuisine type.

> User can add/remove items to/from the cart. User can get all the items of the cart.

> User can place or cancel the order. User can get all the orders ordered by him/her.

> User can apply the coupons. User can get the detailed bill containing tax details.

> User can make a payment using different modes of payment — credit card, wallet, etc.

> Delivery boy can get all the deliveries made by him using his Id.

> User can get the order status anytime. Success, Out for Delivery, Delivered, etc.

#Tables to be created are as follows:

**Restaurant**
```
 Restaurant id — unique for each restaurant
 Restaurant name
 Address
```

**MenuItem**
```
 Menu Id — unique for each
 Name of Item
 Cuisine Type
 Meal Type
 Price
```

**FoodMenu**
```
 Food menu id — unique for each
 Restaurants ids — multiple
 Menu Items — multiple
```

**User**
```
 User id — unique for each
 User name
 Phone no
 Address
``` 

**Order**
``` 
 Order id — unique for each order
 User id — who orders
 Restaurant id — orders from
 Menu Items to be ordered
 Status of Order
```

**Bill**
``` 
 Bill Id — unique for each bill
 Total Cost of the Bill
 Discount applied
 Total tax
 Amount to be paid
```

**Payment**
``` 
 Payment Id — unique for each
 Order Id — for order details
 Amount Paid by user
 Coupon code applied
 Status of Payment
```

**Delivery_Partner**
``` 
 Partner Id — unique for each
 Address
 Phone
 Is_Available
 Location — Current location of delivery partner
```

**Delivery**
``` 
 Delivery Id — unique for each
 Delivery partner Id — User model
 User Id — for address details
 Order Id — for order details
 Delivery Time — for a status update
```

>DataBase which can be used is Postgres

##Explaination for CRUD

```
All the functionalities related to the restaurants will be handled by the Restaurant Service. It will interact with Restaurant Data only. It will render the first page of the application, i.e., the list of all restaurants or the searched restaurants. It will also allow restaurants to register and Admin to manage.

User profile related features will be provided by User Service. It will interact with User Data only. It will allow Customers and Delivery boys to register and update their profiles.

Once the customer selected the restaurant, the second page of the application, i.e., the food menu will be rendered by the Food Menu Service. It will also allow customers to search for the items on the menu basis on some category. It will interact with Food Menu Data only.

Cart Service will allow Customers to add or remove the items in or from the cart. It will render the third page of the application, i.e., items in the cart. It will interact with the Cart Data and will also call the Food Menu Service to get the items using Id. We can use the Command Pattern to handle the add or remove commands.
Onthe cart page, Pricing Service will allow Customers to see the bill details. It will call the Cart Service to get all the items of the cart to render the bill. We can use a Strategy Pattern and have different types of strategies — TwentyPercentOff, FiveHundredOff, etc.

Customers can place or cancel the order, once the cart is finalized, using Order Service. It will interact with Order Data only. It will allow customers to see the order history also. Customers can select the history based on the restaurant also. We can use the Command Pattern to handle place or cancel commands.

Payments can be made to the restaurants using Payment Service. It will interact with the Payment Data and also call the Pricing Service to validate the payment made & the Order Service to update the order status. It will allow Customers to add the Payment against their order.

Delivery Service will deal with all the functionalities related to the order delivery. It will interact with the Delivery Data and also call the Order Service to get the order to be delivered.

```
