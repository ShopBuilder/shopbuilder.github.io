the **Globals** are found in  `window.SBsdk.SBdata`                    
                
To see all of the globals available:          
- open your shopbuilder website        
- open the console and type `console.log(window.SBsdk.SBdata)`         
      
---------------------------------
             
#### Page Data

Page data gives you information about the page you are in.       
All of the page data are found in `window.SBsdk.SBdata.page`     
                 
```   
// @Code        
console.log(window.SBsdk.SBdata.page);          

// @Result
{         
  id: '', // id of product for example (if there is no id by default it will be empty)              
  type: '', // ex. homepage
  action: '', // ex. Add | Edit | View            
  query_strings: '' //ex. ?a=34&b=34         
}      
``` 
        
**page type common values:**  `window.SBsdk.SBdata.page.type`               
1- homepage       
2- collection (for the collection page)     
3- shop_builder_display (for the product page)       
4- page (for basic page)        
5- order (for order page)                
       

**page action common values:** `window.SBsdk.SBdata.page.action`               
1- view             
2- edit      
3- add                          
     
                                  
*In some pages, you might find other extra information in the page data*            
                   
```
 { // In the home page
   type:"homepage",
   action:"view",
   cart_uuid:"..",
   id:"",
   products_on_sale: { [[product_article_id]]: true or false}, // States what products are on sale; this variable only appears if the user added product(s) through panels ex {node-22: true} 
   query_strings:""
 }
 { // In the checkout complete page
  type: 'checkout',
  action: 'complete',
  order: {
    total_amount: '',
    currency_code: '',
    currency_symbol: '',
  }
 { // In the checkout page
  type: 'checkout',
  action: 'checkout',
  order: {
    total_amount: '',
    currency_code: '',
  }
{ // In the order history page
  type: 'order',
  action: 'history view',
  order: {
    order_id: '',
  },
}

```
      
             
---------------------------------
      
#### Website Data    

- Website Data gives information about your website `window.SBsdk.SBdata.SBwebsite_data`    

```  
// @Code       
console.log(window.SBsdk.SBdata.SBwebsite_data);      
// @Result 
{
  website_id //This is gona be the website id ex.1234568789
  user_id //id of user that is currently logged ex. 30       
  user_role //Array of user roles ex. ["Authenticated", "merchant"]                
  map_marker //Array of user roles ex. ["Authenticated", "merchant"]                
}
```
          
       
- **Google Map information:**  

google map info:
 
>  For pages containing a map, the global  `window.SBsdk.SBdata.SBwebsite_data.gmap_object` will represent the google map object that you can manipulate as needed; note that in other pages where the map doesn't exist this global will be empty ie. `window.SBsdk.SBdata.SBwebsite_data.gmap_object = ''`         
               
>  Use this global as per [google maps documentations](https://developers.google.com/maps/documentation/javascript/reference/map).

Example: use the google map function `panBy` will be as follows
```
if(window.SBsdk.SBdata.SBwebsite_data.gmap_object !== ''){
  /* if it is not empty then there is the google maps object!! */
  var map_object = window.SBsdk.SBdata.SBwebsite_data.gmap_object;
  map_object.panBy(500, 100);
}
```

          
google marker info:
 
>  1- To access the marker image being used by the SB platform or a theme app use: `window.SBsdk.SBdata.SBwebsite_data.map_marker.theme`.                  
>  2- To customize your marker using a theme app (ie. overides the one being used in the SB platform) [click here](/sdk/callbacks/#google-map-marker-callback)   
>  3- To set an active marker image url using a 3rd party app, please do set it in the following variable and fetch it from here: `window.SBsdk.SBdata.SBwebsite_data.map_marker.active`.           

---------------------------------
      
#### Page Data Events         
                 
Page data events are information of events that are executed on page load:         
found in `window.SBsdk.SBdata.page.init_event`               
         
Cases where we have this page data event:     

1- After adding a product to cart within product drawer, the page will refresh and fire this event        
                  
```
{
    id: 'Product url alias',
    type: 'cart',
    action: 'new item',
    query_strings: '" . $query_strings_text . "'
}
```      

2- A specific case event is executed only when user login through login popup and a query string after-login-event is available       
               
```
{
    id: 'Value of query string after-login-event',
    type: 'user',
    action: 'after login',
    query_strings: '" . $query_strings_text . "'
 }
```
           
3- If shopbuilder is configured to redirect products, this event will be executed when the redirect happens:      
       
```
{
    id: 'Product url alias',
    type: 'product',
    action: 'product-redirect',
    query_strings: '" . $query_strings_text . "'
  }
```     
     
4- When trying to add an out-of-stock product to cart within product drawer: 
     
```
{
    id: 'Product url alias',
    type: 'cart',
    action: 'out-of-stock',
    query_strings: '" . $query_strings_text . "'
}
```

             
------------------
             