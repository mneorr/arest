# A(wesome) REST debug server

This is a simple application made for testing the HTTP requests.
Confirm what you're sending from a mobile device to a web server.

Just hit the server with the desired HTTP method (GET,POST,DELETE,..) and you should get the parameters passed in back in JSON or XML.

### Example
GET - [JSON](http://log.mneorr.com/json?name=marin&surname=usalj&twitter=@mneorr&sample_array[]=one&sample_array[]=two&sample_array[]=three)
GET - [XML](http://log.mneorr.com/xml?name=marin&surname=usalj&twitter=@mneorr&sample_array[]=one&sample_array[]=two&sample_array[]=three)


For instance, I've used this one to test the BubbleWrap HTTP library.

``` ruby

(main)> BW::HTTP.post('http://log.mneorr.com/json', payload: { name: 'marin'}) { |response| p response.body.to_str }
# =>  "{\"method\":\"POST\",\"params\":{\"name\":\"marin\"}}"

(main)> BW::HTTP.get('http://log.mneorr.com/json?nick=mneorr') { |response| p response.body.to_str }
# =>  "{\"method\":\"GET\",\"params\":{\"nick\":\"mneorr\"}}"


(main)> user = { name: 'marin', twitter: '@mneorr', followers: ['John', 'Mark', 'Ive'] }
# => {:name=>"marin", :twitter=>"@mneorr", :followers=>["John", "Mark", "Ive"]}

(main)> BW::HTTP.get('http://log.mneorr.com/json', payload: user) { |response| p BW::JSON.parse(response.body) }
# =>  {"name"=>"marin", "twitter"=>"@mneorr", "followers"=>["John", "Mark", "Ive"], "method"=>"GET"}

```


#### TODO

Authentications, redirects
