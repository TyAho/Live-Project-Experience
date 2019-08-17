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
    amadeus = Client(
        client_id = "oXoHcPGNhQAKNcvvhFIkB9kFudwrBYTy",
        client_secret = "zs3PhgM4HNpZbCm4"
    )
    response = amadeus.shopping.hotel_offers.get(cityCode = IATA)
    with open("log.json", "w+", encoding="utf-8") as log:
        json.dump(response.data, log, indent=2)
    result = response.data
    print(result[1]['hotel']['name'])
    print(result[1]['hotel']['address']['lines'][0])
    print(result[1]['offers'][0]['price']['base'])
    # print(result[1]['type']['rating'][0])

    context = {
        'name' : result[1]['hotel']['name'],
        'address' : result[1]['hotel']['address']['lines'][0],
        'price' : result[1]['offers'][0]['price']['base']
        # 'price' : result[1]['offers'][0]['price']['base']
        # 'hotel' : result[1]['type']['rating'][0]
    }
    return context
    def hotelIndex(request):       
        if request.method =='POST':
            desResult = request.POST.get('destinationvalue')
            result = hotelSearch(request, desResult)     
            context = result
        
        return render(request, "HotelApp/index.html", {'context' : context})
    else:
        return render(request, "HotelApp/index.html")
# URLS Section 


    from django.urls import path
    from . import views
    from django.views.generic.base import TemplateView

    urlpatterns = [
        path('', views.hotelIndex, name="Hotels")


    ]
    
# Models Section


    class Search(models.Model):
        destination = models.CharField(max_length = 50)

    class HotelApp_search(models.Model):
        destination = models.CharField(max_length = 50)
    #added display items

    class Reviews(models.Model):
        reviews = models.CharField(max_length = 50)

    class HotelName(models.Model):
        name = models.CharField(max_length = 50)

    class Price(models.Model):
        price = models.CharField(max_length = 50)
        
        
# Forms Section
              

    class SearchForm(forms.Form):
        # class Meta:
            search = forms.CharField(label='Enter Your Destination', max_length=60, required=True)

            def clean(self):
                clean_form = self.cleaned_data
                return clean_form

                model = self.search
                fields = ['destination'] 
                labels = {
                    'destination' : 'Your Destination',
                }

    class PriceForm(forms.Form):
        price = forms.CharField(label='', max_length=60, required=True)

        def clean(self):
                clean_form = self.cleaned_data
                return clean_form
        
# Job Management Story
# Adding Preloader 


# Creating the preloader with Controller and View 
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;

    namespace ManagementPortal.Controllers
    {
        public class PreLoaderController : ApplicationBaseController
        {
            // GET: PreLoader
            public ActionResult Save()
            {
                return View();
            }
        }
    }
    
    
    
        @{
        ViewBag.Title = "Save";
    }

    <script src="~/Scripts/jquery-1.10.2.js"></script>
    <h2>Welcome To Ajax Loader</h2>
    <div id="divLoader" style="display:none;">
        <img src="~/Content/ajax-loader.gif" alt="Loader" />
    </div>
    <input type="submit" id="btnSubmit" value="Submit" />
    <script>
        $("#btnSubmit").click(function () {
            $("#divLoader").show();
            $.ajax({
                url: '/Test/Submit',
                dataType: "json",
                type: "POST",
                contentType: 'application/json; charset=utf-8',
                data: {},
                //async: true,
                //processData: false,
                // cache: false,
                success: function (data) {
                    $("#divLoader").hide();
                    alert(data);
                },
                error: function (xhr) {
                    $("#divLoader").hide();
                    alert('error');
                }
            })
        });
    </script>
    


# Creating seperate button for the preloader functionality
    break;
    case ButtonType.Save:
        <a type="button" class="btn-sm btn-primary" href="@Url.Action(Model.Action, new { id = Model.RouteId})">
            <span><i class="fa fa-pencil"></i> Submit </span>
        </a>
        break;
        
        
      case ButtonType.Save:
          result.Buttons.Add(new AnchorButtonVM() { ButtonType = ButtonType.Save, Action = "Save",                           RouteId = routeId });
          break;
# Fixing Home button on navbar of Job management site
The other assignment I was tasked with was to figure out why the home button on the navbar was not correctly transferring the users. I was able to fix this by changing the href to the correct corresponding URL.
    <div class="card text-light bg-secondary py-3 px-2">
                        <h5 class="card-title">Looking for our main website?</h5>
                        <input type="button" class="home_btn" onclick="location.href='@Url.Action("Dashboard",         "Home")'" value="Take a look">
                    </div>
