# geo class

Class to get geo decode lat-lng to metters and vice versa in rectangle cluster

## Usage

In django can use this method like:

````python

 def find_object(lat, lng, radius, sort_by):
    center = LatLng(lat, lng)

    max_lat = center.destination_point_north(radius).lat
    min_lat = center.destination_point_south(radius).lat
    max_lng = center.destination_point_east(radius).lng
    min_lng = center.destination_point_west(radius).lng

    # find all objects inside the given rectangle

    objects = Objecta.objects.filter(
                   lat__lte = max_lat,
                   lat__gte = min_lat,
                   lng__lte = max_lng,
                   lng__gte = min_lng).all()


    # function that returns the distance from the object to the
    # center point
    distance_to_center = lambda st: center.distance_to(st.get_location())
    # function that returns true if the object is within the
    # radius
    is_within_radius = lambda st: (distance_to_center(st) <= radius)

    objects = filter(is_within_radius, objects)

    # Sort gas stations by given parameter
    objects = sort_object_by(objects, sort_by, distance_to_center, 1)

    objects = list(objects)

    return objects

````

   


