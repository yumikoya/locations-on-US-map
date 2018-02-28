# locations-on-US-map
plotting locations by cities on the map of North America with state borders

# Draw the locations of cities on a map of the US

import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap
from geopy.geocoders import Nominatim
import math

cities = [["Vancouver", 3],["Cupertino", 3],["Irvine", 3],["Mountain View", 3] ,["River View", 3], ["Chicago",6]
    ,["Somerville", 3]
    ,["Grand Central", 3]
    ,["Midtown", 3]
    ,["Union Square", 3]
    ,["Providence", 3]
    ,["El Paso", 3]
    ,["Houston",6]
    ,["Annandale", 3]
    ,["Bellevue", 3]
    ,["Seattle", 3]]
          
mcities = [["Phoenix, AZ", 3]
    ,["Scottsdale, AZ", 3]
    ,["San Francisco", 3]
    ,["Greenwich, CT", 3]
    ,["Hartford, CT", 3]
    ,["Wilton, CT", 3]
    ,["Washington DC", 3]
    ,["Miami", 3]
    ,["Tampa", 3]
    ,["Fort Lauderdale", 3]
    ,["Atlanta", 3]
    ,["New Orleans", 3]
    ,["Harvard Sq", 3]
    ,["Ann Arbor, MI", 3]
    ,["Grand Rapids, MI", 3]
    ,["Troy, MI", 3]
    ,["Raleigh, NC", 3]
    ,["Hoboken, NJ", 6]
    ,["Brooklyn, NY", 6]
    ,["Columbus, OH", 3]
    ,["Philadelphia", 3]
    ,["Knoxville, TN", 3]
    ,["Austin, TX", 3]
    ,["Dallas, TX", 3]
    ,["San Antonio, TX", 3]
    ,["North Dallas, TX", 3],["Austin,TX", 3]]          

scale = 5

map = Basemap(llcrnrlon=-119,llcrnrlat=22,urcrnrlon=-64,urcrnrlat=49,
        projection='lcc',lat_1=32,lat_2=45,lon_0=-95)

# load the shapefile, use the name 'states'
map.readshapefile('ne_50m_admin_1_states_provinces', name='states', drawbounds=True)

# Get the location of each city and plot it
geolocator = Nominatim()
for (city,count) in cities:
    loc = geolocator.geocode(city)
    x, y = map(loc.longitude, loc.latitude)
    map.plot(x,y,marker='o',color='Red',markersize=int(math.sqrt(count))*scale)
    

for (city,count) in mcities:
    loc = geolocator.geocode(city)
    x, y = map(loc.longitude, loc.latitude)
    map.plot(x,y,marker='o',color='Blue',markersize=int(math.sqrt(count))*scale)    

plt.show()
