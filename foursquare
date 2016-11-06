import httplib2
import json
import sys
import codecs

sys.stdout = codecs.getwriter('utf8')(sys.stdout)
sys.stderr = codecs.getwriter('utf8')(sys.stderr)
google_api_key = "AIzaSyBWPfzt6oZm9VxWFMI7FWY12J8zX1S9hyw"
foursquare_client_id = "YREEJO50WCOOJLRALKPQFYZQLVZDXMQGJN32SFXLFRXUQKMU"
foursquare_client_secret = "NOKGDWMUGFKECBMAJVQCQ2TK1SXGRNUJSW1CFYCKIAEIXYAP"


def getGeocodeLocation(inputString):


    locationString = inputString.replace(" ", "+")
    url = ('https://maps.googleapis.com/maps/api/geocode/json?address=%s&key=%s'% (locationString, google_api_key))
    h = httplib2.Http()
    result = json.loads(h.request(url,'GET')[1])
   # print "response HEader %s \n \n" %result
    latitude = result['results'][0]['geometry']['location']['lat']
    longitude = result['results'][0]['geometry']['location']['lng']
    return (latitude,longitude)


def findARestaurant(mealType,location):

	latitude, longitude = getGeocodeLocation(location)
	url = ('https://api.foursquare.com/v2/venues/search?client_id=%s&client_secret=%s&v=20130815&ll=%s,%s&query=%s' % (foursquare_client_id, foursquare_client_secret,latitude,longitude,mealType))
	h = httplib2.Http()

	result = json.loads(h.request(url,'GET')[1])
        #print result


        if result['response']['venues']:


                    restaurant = result['response']['venues'][x]
                    venue_id = restaurant['id']
                    restaurant_name = restaurant['name']
                    restaurant_address = restaurant['location']['formattedAddress']

                    address = ""
                    for i in restaurant_address:
                        address += i + " "
                    restaurant_address = address
                    url = ('https://api.foursquare.com/v2/venues/%s/photos?client_id=%s&v=20150603&client_secret=%s' % ((venue_id,foursquare_client_id,foursquare_client_secret)))
                    result = json.loads(h.request(url, 'GET')[1])

                    if result['response']['photos']['items']:
                        firstpic = result['response']['photos']['items'][0]
                        prefix = firstpic['prefix']
                        suffix = firstpic['suffix']
                        imageURL = prefix + "1920x1080" + suffix


                    restaurantInfo = {'name':restaurant_name, 'address':restaurant_address, 'image':imageURL}
                    print "Restaurant Name: %s" % restaurantInfo['name']
                    print "Restaurant Address: %s" % restaurantInfo['address']
                    print "Image: %s \n" % restaurantInfo['image']
                    return restaurantInfo
        else:
                    print "No Restaurants Found for %s" % location
                    return "No Restaurants Found"

if __name__ == '__main__':


    for x in range(0, 1):
        print (x + 1)
        findARestaurant(" ", " ghatkopar east")

