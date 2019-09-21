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
For my project on C# I was tasked with the creation of a preloader for each create and edit view, so that the user would know there was a response to their input. In making this preloader I had to create a controller and view for the preloader itself and than I followed this up by creating a serperate button in the common data folder in reference to this preloader, so that the create and edit views could easily use the button. Below is the code I made for this assignment.  

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
                        <input type="button" class="home_btn" onclick="location.href='@Url.Action("Dashboard", "Home")'" value="Take a look">
                    </div>
# Front End for Job Management Story
In the front end portion of the live project I was assigned with the job of fixing the Company News dashboard layout, as when too many news story items were added, the cards shapes would transform so that they were not all equal in size. In addition, the cards were very narrow and it was hard to read exactly what was on them, so I needed to widen them as well. The other assignment I worked on was to fix the Company News Index, as this was also poorly laid out, since the button group did not line up horizontally and each new news item took up a lot more space than was needed. 

# Fixing the Company News Dashboard Layout 
    /****Company News Cards****/
    #news-header {
        background-color: rgb(117, 137, 138);

    }

    #new-body {
        background-color: rgb(219, 228, 227);
        padding: 15px 0px 0px 80px;


    }
        #new-body .card {
            box-shadow: 5px 7px var(--dark-grey);
            padding: 15px 20px 40px 10px;


            width: 330px;

        }
    .col {

        flex-grow: 0;
        max-width: 100%;

    }
    
# Fixing the Company News Index 
    /****Styling for Company News/Jobs Index****/

    .IndexBody {
        background-color: rgba(255, 255, 255,0.8);
    }

    #news-body {
        background-color: rgba(255, 255, 255,0.8);
        margin-right: -200px;
        margin-left: -233px;    
    }



    .no-gutters {
        padding: 0px -1px 40px 225px;
        margin-left: 0px;
        margin-right: 50px;
        box-sizing: content-box;
        padding: 20px;
    }
# Back End for Job Management Story
In the back end portion of the live project I was was assigned with the job of creating a personal profile page, by connecting each user id to the database from a one to one relationship, for the user to add additional information about themselves. In addition I was also tasked with adding additional sorting, filtering and paging functionality to the jobsite page, so that the view would be easier to work with and allowed the page itself to be scalable as the data being transferred into it grew. 


# Adding personal profile and functionality
# Adding model
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.DataAnnotations;
    using System.ComponentModel.DataAnnotations.Schema;
    using System.Linq;
    using System.Web;

    namespace ManagementPortal.Models
    {
        public class PersonalProfile
        {

            [Key]
            [ForeignKey("Person")]
            public string ProfileID { get; set; }

            [Required]
            [MaxLength(100)]
            [StringLength(100, MinimumLength = 1, ErrorMessage = "About Me must be between 1 and 100 characters")]
            [Display(Name = "AboutMe")]
            public string AboutMe { get; set; }


            [Required]
            [StringLength(50, MinimumLength = 1, ErrorMessage = "Tagline must be between 1 and 100 characters")]
            [Display(Name = "Tagline")]
            public string TagLine { get; set; }

            public virtual ApplicationUser Person { get; set; }

            public static implicit operator PersonalProfile(string v)
            {
                throw new NotImplementedException();
            }
        }
    }
    
# Adding controller and view

    using System;
    using System.Collections.Generic;
    using System.Data;
    using System.Data.Entity;
    using System.Linq;
    using System.Net;
    using System.Web;
    using System.Web.Mvc;
    using ManagementPortal.Models;

    namespace ManagementPortal.Controllers
    {
        public class PersonalProfilesController : ApplicationBaseController
        {
            private ApplicationDbContext db = new ApplicationDbContext();

            // GET: PersonalProfiles
            public ActionResult Index()
            {
                var personalProfiles = db.Profile.Include(p => p.Person);
                return View(personalProfiles.ToList());
            }

            // GET: PersonalProfiles/Details/5
            public ActionResult Details(string id)
            {
                if (id == null)
                {
                    return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
                }
                PersonalProfile PersonalProfiles = db.Profile.Find(id);
                if (PersonalProfiles == null)
                {
                    return HttpNotFound();
                }
                return View(PersonalProfiles);
            }

            // GET: PersonalProfiles/Create
            public ActionResult Create()
            {
                ViewBag.ProfileID = new SelectList(db.Users, "Id", "DisplayName");
                return View();
            }

            // POST: PersonalProfiles/Create
            // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
            // more details see https://go.microsoft.com/fwlink/?LinkId=317598.
            [HttpPost]
            [ValidateAntiForgeryToken]
            public ActionResult Create([Bind(Include = "ProfileID,AboutMe,TagLine")] PersonalProfile PersonalProfiles)
            {
                if (ModelState.IsValid)
                {
                    db.Profile.Add(PersonalProfiles);
                    db.SaveChanges();
                    return RedirectToAction("Index");
                }

                ViewBag.ProfileID = new SelectList(db.Users, "Id", "DisplayName", PersonalProfiles.ProfileID);
                return View(PersonalProfiles);
            }

            // GET: PersonalProfiles/Edit/5
            public ActionResult Edit(string id, string ProfileID)
            {
                //var ProfileID = Request.QueryString["id"];
                //return View();



                if (id == null)
                {
                    return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
                }
                PersonalProfile PersonalProfiles = db.Profile.Find(id);
                if (PersonalProfiles == null)
                {
                    return HttpNotFound();
                }
                ViewBag.ProfileID = new SelectList(db.Users, "ProfileID", "DisplayName", PersonalProfiles.ProfileID);
                return View(PersonalProfiles);
            }

            // POST: PersonalProfiles/Edit/5
            // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
            // more details see https://go.microsoft.com/fwlink/?LinkId=317598.
            [HttpPost]
            [ValidateAntiForgeryToken]
            public ActionResult Edit([Bind(Include = "ProfileID,AboutMe,TagLine")] PersonalProfile PersonalProfiles, IndexViewModel ProfileID)
            {
                //var ProfileID = Request["ProfileID"];
                //var AboutMe = Request["About Me"];
                //var TagLine = Request["TagLine"];

                //return RedirectToAction(ProfileID);


                if (ModelState.IsValid)
                {
                    db.Entry(PersonalProfiles).State = EntityState.Modified;
                    db.SaveChanges();
                    return RedirectToAction("Index");
                }
                ViewBag.ProfileID = new SelectList(db.Users, "ProfileID", "DisplayName", PersonalProfiles.ProfileID);
                return View(PersonalProfiles);
            }

            // GET: PersonalProfiles/Delete/5
            public ActionResult Delete(string id)
            {
                if (id == null)
                {
                    return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
                }
                PersonalProfile PersonalProfiles = db.Profile.Find(id);
                if (PersonalProfiles == null)
                {
                    return HttpNotFound();
                }
                return View(PersonalProfiles);
            }

            // POST: PersonalProfiles/Delete/5
            [HttpPost, ActionName("Delete")]
            [ValidateAntiForgeryToken]
            public ActionResult DeleteConfirmed(string id)
            {
                PersonalProfile PersonalProfiles = db.Profile.Find(id);
                db.Profile.Remove(PersonalProfiles);
                db.SaveChanges();
                return RedirectToAction("Index");
            }

            protected override void Dispose(bool disposing)
            {
                if (disposing)
                {
                    db.Dispose();
                }
                base.Dispose(disposing);
            }
        }
    }
    
    
  # create view
        @model ManagementPortal.Models.PersonalProfile

    @{
        ViewBag.Title = "Create";
    }

    <h2>Create</h2>

    @using (Html.BeginForm()) 
    {
        @Html.AntiForgeryToken()

        <div class="form-horizontal">
            <h4>PersonalProfile</h4>
            <hr />
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            <div class="form-group">
                @*@Html.HiddenFor(m => m.ProfileID, new { id = "Person" })*@
                @Html.LabelFor(model => model.ProfileID, "ProfileID", htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.DropDownList("ProfileID", null, htmlAttributes: new { @class = "form-control" })
                    @*@Html.HiddenFor(m => m.ProfileID, new { id = "Person" })*@
                    @Html.ValidationMessageFor(model => model.ProfileID, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.AboutMe, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.AboutMe, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.AboutMe, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.TagLine, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.TagLine, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.TagLine, "", new { @class = "text-danger" })
                </div>
            </div>


            <div class="form-group">
                <div class="col-md-offset-2 col-md-10">
                    <input type="submit" value="Create" class="btn btn-default" />
                </div>
            </div>
        </div>
    }

    <div>
        @Html.ActionLink("Back to List", "Index")
    </div>
# connecting to the IdentityModels model from the PersonalProfile model in order to create a one to one relationship for the user id
I added the public virtual PersonalProfile Profile { get; set; } line of code in order to create the relationship, and than added the public DbSet<PersonalProfile>Profile { get; set; } into the ApplicationDbContext to connect to that database so that each user would show up in the database.
    
    
    public class ApplicationUser : IdentityUser
        {

            // PROFILE PICTURE
            public byte[] ProfilePicture { get; set; }

            //Set DisplayName with first name and last initial
            public string DisplayName { get { return FirstName + " " + LastName.Substring(0, 1); } internal set { FirstName = value; LastName = value; } }
            [Required(ErrorMessage = "Required Field. Please enter a First Name:"), Display(Name = "First Name")]
            public string FirstName { get; set; }
            [Required(ErrorMessage = "Required Field. Please enter a Last Name: "), Display(Name = "Last Name")]
            public string LastName { get; set; }
            [Required(ErrorMessage = "Required Field. Please enter a Work Type >> Leadman,Foreman,ExpMBA, or NewMBA: "), Display(Name = "Work Type")]
            public WorkType WorkType { get; set; }
            public string UserRole { get; set; }
            [Display(Name = "Suspended")]
            public bool Suspended { get; set; }

            public string FullName { get { return (FirstName + " " + LastName); } }
            public virtual List<Job> Jobs { get; set; }
            public virtual List<Schedule> Schedules { get; set; }
            public virtual PersonalProfile Profile { get; set; }
            public async Task<ClaimsIdentity> GenerateUserIdentityAsync(UserManager<ApplicationUser> manager)
            {
                // Note the authenticationType must match the one defined in CookieAuthenticationOptions.AuthenticationType
                var userIdentity = await manager.CreateIdentityAsync(this, DefaultAuthenticationTypes.ApplicationCookie);
                // Add custom user claims here
                return userIdentity;
            }
            //add the user identity here for the aspnetuser table.

        }
        
        
        
                                   
        
    public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
        {
            public ApplicationDbContext()
                : base("DefaultConnection", throwIfV1Schema: false)
            {
            }

            // Begin DbSets

            public DbSet<CalendarEvent> CalendarEvents { get; set; }
            public DbSet<CreateUserRequest> CreateUserRequests { get; set; }

            public DbSet<ChatMessage> ChatMessages { get; set; }

            public DbSet<CompanyNews> CompanyNews { get; set; }

            public DbSet<Job> Jobs { get; set; }
            public DbSet<JobSite> JobSites { get; set; }
            public DbSet<ShiftTime> ShiftTime { get; set; }
            public DbSet<JobOther> JobOthers { get; set; }

            public DbSet<Schedule> Schedules { get; set; }
            //public DbSet<EventModel> Events { get; set; }
            public DbSet<PersonalProfile>Profile { get; set; }
            //public virtual DbSet<CalEvent> CalendarEvents { get; set; }

            // End DbSets       
            
            
