# Live-Project-Experience
# Introduction
In starting on my Live Project, we worked for two weeks with python, focusing on the front end code for a travel app.
Using Python and a virtual environment, I was able to go back and check each change I made to the source code in order to figure out my mistakes. Each person on the team also worked on stories for the flight app, and overall we were able to make a very functional program that we were all proud of. Much of the stories we worked on required us to do our own research and take in as much information as possible in order to progress thorugh the project, as a lot of the coding assignments we had no prior experience with. This project also was a good way for each and everyone of us to gain the knowledge needed for what a real world coding job would be like. Each day we took turns sharing what we did the previous day, and what challenges we faced, as well as what we were going to work on that day. This helped  give everyone an idea as to where we were and how we could work together in order to fix any of the issues we faced.

In the space below are some of the assignments I worked on throughout the live project.


# Flight App Story
# Hotel App Clean-Up
In the Python Live Project, I was assigned the job of reworking the Hotel App, and adding more functionality so that the user would actually see the correct information displayed based off of the destination they entered. 

# Working with the Amadeus API to get the correct information displayed
The Hotel App originally had no relevant information appear after searching for a destination. So my job was to make the API respond with the correct information for the user. I added the data that would give the user a better idea as to what kind of hotels were in the area they were visiting. The information displayed was the hotel prices, names, and reviews.


    def hotelSearch(request, IATA):
        form = SearchForm(initial = "")
       //Initialize Amadeus
        amadeus = Client(
            client_id = "oXoHcPGNhQAKNcvvhFIkB9kFudwrBYTy",
            client_secret = "zs3PhgM4HNpZbCm4"
        )
        response = amadeus.shopping.hotel_offers.get(cityCode = IATA)
        with open("log.json", "w+", encoding="utf-8") as log:
            json.dump(response.data, log, indent=2)
        result = response.data
        print (result)
        context = {'form' : form, 'results' : result}
        return render(request, "HotelApp/index.html", context)

    def hotelPrice(request, IATA):
        price = PriceForm(initial = "")
       //Initialize Amadeus
        amadeus = Client(
            client_id = "oXoHcPGNhQAKNcvvhFIkB9kFudwrBYTy",
            client_secret = "zs3PhgM4HNpZbCm4"
        )
        response = amadeus.shopping.hotel_offers.get(price = IATA)
        with open("log.json", "w+", encoding="utf-8") as log:
            json.dump(response.data, log, indent=2)
        result = response.data
        print (result)
        // context = {'form' : price, 'results' : result}
        price = PriceForm['price']
        return render(request, 'HotelApp/index.html', {'price' : PriceForm, 'results' : result})#, PriceForm)  


    def hotelName(request, IATA):
        form = SearchForm(initial = "")
       //Initialize Amadeus
        amadeus = Client(
            client_id = "oXoHcPGNhQAKNcvvhFIkB9kFudwrBYTy",
            client_secret = "zs3PhgM4HNpZbCm4"
        )
        response = amadeus.shopping.hotel_offers.get(name = IATA)
        with open("log.json", "w+", encoding="utf-8") as log:
            json.dump(response.data, log, indent=2)
        result = response.data
        print (result)
        context = {'form' : form, 'results' : result}
        return render(request, "HotelApp/index.html", context)

    def hotelReview(request, IATA):
        form = SearchForm(initial = "")
       //Initialize Amadeus
        amadeus = Client(
            client_id = "oXoHcPGNhQAKNcvvhFIkB9kFudwrBYTy",
            client_secret = "zs3PhgM4HNpZbCm4"
        )
        response = amadeus.shopping.hotel_offers.get(rating = IATA)
        with open("log.json", "w+", encoding="utf-8") as log:
            json.dump(response.data, log, indent=2)
        result = response.data
        print (result)
        context = {'form' : form, 'results' : result}
        return render(request, "HotelApp/index.html", context)
    
    
       def hotelIndex(request):
        //Creates blank form on initial page load
        if request.method == 'GET':
        
        form = SearchForm(initial = "")
        context = {'form' : form}
        return render(request, "HotelApp/index.html", context)
            
    elif request.method =='POST':
        
        form = SearchForm(request.POST)
        // form.save()
        global search
        global cities
        
        search = "search.objects.filter().order_by('-id')[0]"
        cities = "findMatches(search.destination)"
        context = {'cities' : cities, 'form': form}
        return render(request, "HotelApp/index.html", context)
