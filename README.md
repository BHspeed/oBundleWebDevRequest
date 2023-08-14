# oBundleWebDevRequest
***PREVIEW CODE****
(preview code: n8c2f7fvdo)
# My BigCommerce Requested Project

This project is a demonstration of my skills in [specific technologies or platforms]. It showcases [brief overview].

## Bigcommerce Store Preview

- https://github.com/BHspeed/oBundleWebDevRequest/blob/925748394bb4018835dc432eadfdf656580ae0b1/_productView.scss#L13-L61
- https://github.com/BHspeed/oBundleWebDevRequest/blob/925748394bb4018835dc432eadfdf656580ae0b1/card.html#L61-L91)
- https://github.com/BHspeed/oBundleWebDevRequest/blob/925748394bb4018835dc432eadfdf656580ae0b1/category.html#L66-L234
- ------------------------------------------------------------------------------------------------------------------

Button Rendering:

The code checks if the current page is part of the "Special Items" category.
If it is, two buttons are displayed:
The "Add All To Cart" button.
The "Remove All Items" button (which is initially hidden).
JavaScript Enhancements:

storefrontCall Function:

A function to interact with the BigCommerce API. It makes different types of requests (like GET, POST) to given endpoints and can also send data.
createCart Function:

This function attempts to add items to the cart. If it's successful, you're notified that products were added. If there's an issue, you'll get an alert indicating the problem.
checkCartItems Function:

This function checks if there are items in the cart, either digital or physical.
updateButtonDisplay Function:

Based on whether there are items in the cart, it decides if the "Remove All Items" button should be visible or hidden.
DOMContentLoaded Event:

Once the web page is fully loaded:
It checks if there are items in the cart and decides the visibility of the "Remove All Items" button.
If the "Add All To Cart" button is clicked, it fetches all product IDs from the page and tries to add them to the cart. After adding, it rechecks the cart status and updates the button visibility.
'specialButton' Click Event:

If you click on the "Remove All Items" button:
It fetches the current cart and all its items.
For every item in the cart, it sends a request to remove that item.
After removing items, it updates the button visibility.


-----------------------------------------------------------------------------

- **URL**: [Your Bigcommerce Store URL](https://obundle-demo-request.mybigcommerce.com/)

Please note that the preview code may change, so if there are any issues accessing the store, kindly contact me.
