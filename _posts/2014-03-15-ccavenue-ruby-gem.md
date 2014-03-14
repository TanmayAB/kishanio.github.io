---
layout: post
title: CCAvenue Ruby Gem
sitemap:
  lastmod: 2014-03-15
  priority: 0.7
  changefreq: monthly
---

**Motivation**

I wrote this [Gem](http://rubylearning.com/blog/2010/12/14/ruby-gems-—-what-why-and-how/)  whilst working on [printajoy](http://printajoy.com). It enables you integrate [CCAvenue Payment Gateway](http://ccavenue.com) with your existing Ruby application.

**What is a Gem?**

Gem are packages that work as standalone application or can be used to enhance functionality of existing application.

**Research**

1. [Active Merchant CCAvenue](https://github.com/meshbrain/active_merchant_ccavenue) - At first shot it didn't work. Beside it relies on Active Merchant. 

**Download**

Rubygems.org: [https://rubygems.org/gems/ccavenue](https://rubygems.org/gems/ccavenue)

Github: [http://github.com/kishanio/CCAvenue-Ruby-Gem](http://github.com/kishanio/CCAvenue-Ruby-Gem)

**Usage**

Pre-requistes: 

1. Merchant Id
2. Merchant Working Key
3. Redirect Url

All the above three are available on the [CCAvenue Merchant Dashboard](https://mars.ccavenue.com/mer_register/memberLogin_ccav.jsp?logintype=m)

This should just work fine.

```bash
$ gem install ccavenue
```

*Rails* Specific Installation.

Gemfile

```yaml
gem 'ccavenue'
```

Call bundle install

```bash
$ bundle install
```

application_controller.rb
    
```ruby
# Create an instance with merchantid, workingkey and redirect url as parameter
def ccavenue
    return @ccavenue = Ccavenue::Payment.new(<TODO: MERCHANT ID>,<TODO: MERCHANT WORKING KEY>,<TODO: REDIRECT URL>)
end
```


Orders page from which user will be redirected to payment gateway.
 
```ruby   
def send_to_ccavenue
    
    
    # Merchant id needed in view
    @CCAVENUE_MERCHANT_ID = <TODO: MERCHANT ID>
    
    # CCAvenue requires a new order id for each request 
    # so if transaction fails we can use #same ones again accross our website.
    order_id =  Time.now.strftime('%d%m%H%L') + <TODO: Order Id>
    
    # Parameters:
    #
    #   order_id
    #   price
    #   billing_name
    #   billing_address
    #   billing_city
    #   billing_zip
    #   billing_state
    #   billing_country
    #   billing_email
    #   billing_phone
    #   billing_notes
    #   delivery_name
    #   delivery_address
    #   delivery_city
    #   delivery_zip
    #   delivery_state
    #   delivery_country
    #   delivery_email
    #   delivery_phone
    #   delivery_notes
    #
    #
    #   Mandatory - order_id,price,billing_name,billing_address,billing_city,billing_zip,billing_state,billing_country,billing_email,billing_phone
    #   Optional - billing_notes,delivery_name,delivery_address,delivery_city,delivery_zip,delivery_state,delivery_country,delivery_email,delivery_phone,delivery_notes
    
    # Creating encrypted data
    @encRequest = ccavenue.request(order_id,<TODO: Price>,@order.full_name,"#{@order.address1} ,#{@order.address2}",@order.city,@order.zip,@order.state,@order.country,@order.email,@order.phone)

    render "<TODO: Redirect Page>"
end
```

A redirect view has to be renderend that creates a post request for the payment gateway.

```html
<form id="redirect" method="post" name="redirect" action="http://www.ccavenue.com/shopzone/cc_details.jsp">
    <input type="hidden" name="encRequest" value="<%= @encRequest %>">
    <input type="hidden" name="Merchant_Id" value="<%=@CCAVENUE_MERCHANT_ID%>">
</form>

<script>
    document.getElementById("redirect").submit();   
</script>
```

CCAvenue confirmation method. This is called by CCAvenue upon callback.


```ruby    
# Method post 
def payment_confirm  

    # parameter to response is encrypted reponse we get from CCavenue
    authDesc,verify,data = ccavenue.response(params['encResponse'])
    
    # Return parameters:
    #   Auth Description: <String: Payment Failed/Success>
    #   Checksum Verification <Bool: True/False>
    #   Response Data: <HASH/Array: Order_id, amount etc>
    
    
    
    order_Id = data["Order_Id"][0]
    
end
```
    
**Licence**

It's Licenced under [MIT](https://raw.github.com/kishanio/CCAvenue-Ruby-Gem/master/LICENSE.txt)