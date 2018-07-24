# Web API: the good parts (part 1)

babygoat@twreporter.org

2018.07.26

---
## URI design 

* URI naming guidelines
        * Short and easy to type
	* Human readable
	* Do not mix upper and lower case path
	* Hackable
	* Do not expose server side architecture
	* Single naming rule

---
### Short and easier to type

- [x] http://api.example.com/service/api/search

- [v] http://api.example.com/search

---
### Human readable

* Don't overplay first rule
	* e.g., products => prods

* Always use english vocabulary
	* [ProgrammableWeb](https://www.programmableweb.com)

* Avoid typos
	* e.g., carendar => calendar

---
### Don't mix upper and lower case path

* RFC 7230 states that only scheme and host are case sensitive

* Use lower case as standard
	* [x] http://api.example.com/Users/12345
	* [v] http://api.example.com/users/12345

* Real world case
	* Tumblr, Foursquare: 404 not found
	
---
### Hackable

* http://api.example.com/blog/100

* http://api.example.com/blog/2008/04/20/title

---
### Do not expose server side architecture

* http://api.example.com/cgi-bin/get_user.php?user=100
	* might be vulnerable to [cgi-bin attack](http://php.net/manual/en/security.cgi-bin.attacks.php)

---
### Single naming rule

* e.g., Send message to friend id:100
	* http://api.example.com/friends/100/message

* Get message from friend id: 100
	* [v] http://api.example.com/friends/100
	* [x] http://api.example.com/friends?id=100

---
## HTTP Methods

* Operation on Resource 
	* GET
	* POST
	* PUT
	* DELETE
	* PATCH

---
### POST v.s. PUT v.s. PATCH

* POST "creates" a new item under resource collections
	* POST https://api.example.com/v1/products

* PUT "fully updates" or "overwrites" an existing item of resource
	* PUT https://api.example.com/v1/products/123

---
### POST v.s. PUT v.s. PATCH (CONT.)

* PATCH "partially updates" an existing item of resource
	* PATCH https://api.example.com/v1/products/123
	* Body should be descriptions of changes (RFC 5789)
		* [{"op":"replace", "path":"/price", "value":100}] (RFC 6901, JSON Pointers)
        * JSON Merge format can also be applied.

---
## HTML Form

* Only support GET/POST
	* What if we want to do partially update or delete?

* POST Meta data
	* X-HTTP-Method-Override
	* _method

---
### X-HTTP-Method-Override

```
POST /v1/users/123 HTTP/1.1
Host: api.example.com
X-HTTP-Method-Override: DELETE
``` 

---
### _method

* Majorly used in form
	* application/x-www-form-urlencoded

```
<form method="POST" ...>
	<input type="hidden" name="_method" value="PUT">
	...
</form>
```

---
## Endpoint design

* "Resource collection" + "Item"
	* /v1/users
	* /v1/users/:id

* TIPs
	* Plural nouns
	* Be careful with the vocabulary
	* Avoid space and percent-encoded endpoint
	* Use "-" to concatenate all the words

---
## Query parameter design

* Pagination

* Filter

---
### Pagination

* Relative position
	* page/per_page
		* ?page=1&per_page=20
	* offset/limit (more flexible)
		* ?offset=100&limit=120

* Absolute position
	* cursor
		* e.g., Youtube: pulishedBefore=2018-07-25T23:59:59Z	

---
### Filter

* /search as portion of URI?
	* e.g., https://api.twitter.com/1.1/search/tweets.json?q=%23&lang=ja


---
### Filter(Cont.)

* Use query paramter or within URI
	* Unique identified resource
		* /users?id=123
		* /users/123
	* Ignorable
		* /products?page=1&per_page=20
