# C-LiveProject-TheaterCMS

## Create and Style Donation Page

Change the Donate View in the Home View folder.  This page should have several fields that let the user enter their information and donation amount.  The input fields should be in a form.  Take a look at the gif below to see how it should be styled.  Use Bootstrap's Grid Layout to create the layout of the page. The client wants an image displayed behind the title as well, and the font of the title should be Broadway. Add placeholders to every field a user can fill in. You do not need to implement the controller method for the form.

```
    <div class="container" style="font-family: Broadway">
        <div class="jumbotron mb-0" style="background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), 
                                       url('/Content/images/theater.jpg'); 
                                       background-repeat: no-            
                                       repeat; background-size: cover; background-position: 50% 75%">
            <h1 class="text-center">Consider Making a Donation</h1>
        </div>

        <div class="p-3 cms-bg-main-light rounded">
            <form>
                <div class="form-group row">
                    <label for="#" class="col-lg-3 col-form-label">Name*</label>
                    <div class="col-md">
                        <input type="text" class="form-control" placeholder="First Name" />
                    </div>
                    <div class="col-md">
                        <input type="text" class="form-control mt-2 mt-md-auto" placeholder="Last Name" />
                    </div>
                </div>

                <div class="form-group row">
                    <label for="emailAddress" class="col-lg-3 col-form-label">Email Address*</label>
                    <div class="col-lg-9">
                        <input type="text" class="form-control" id="emailAddress" placeholder="Email Address">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="address" class="col-lg-3 col-form-label">Address</label>
                    <div class="col-lg-9">
                        <input type="text" class="form-control" id="address" placeholder="Address">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="donationAmount" class="col-lg-3 col-form-label">Donation Amount($)*</label>
                    <div class="col-lg-9">
                        <input type="number" class="form-control" id="donationAmount" placeholder="Donation Amount">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="donationComments" class="col-lg-3">Donation Comments</label>
                    <div class="col-lg-9">
                        <textarea class="form-control" id="donationComments" placeholder="Place comments here..."></textarea>
                    </div>
                </div>
                <button type="submit" class="btn cms-bg-light">Submit</button>
            </form>
        </div>
    </div>
```

## Create entity model and CRUD Page
***
### Model
```
    public enum prodPosition
    {
        Actor, Director, Technician, StageManager, Other
    }
    public class ProductionMember
    {
        public int ProductionMemberId { get; set; }
        public String Name { get; set; }
        public int? YearJoined { get; set; }
        public prodPosition MainRole { get; set; }
        public String Bio { get; set; }
        //public Byte[] Photo { get; set; }
        public bool CurrentMember { get; set; }
        public String Character { get; set; }
        public int? CastYearLeft { get; set; }
        public int? DebutYearLeft { get; set; }
    }
    
```
### Controller
```
    public class CastMembersController : Controller
    {
        private ApplicationDbContext db = new ApplicationDbContext();

        // GET: Prod/CastMembers
        public ActionResult Index()
        {
            return View(db.CastMembers.ToList());
        }

        // GET: Prod/CastMembers/Details/5
        public ActionResult Details(int? id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
            CastMember castMember = db.CastMembers.Find(id);
            if (castMember == null)
            {
                return HttpNotFound();
            }
            return View(castMember);
        }

        // GET: Prod/CastMembers/Create
        public ActionResult Create()
        {
            return View();
        }

        // POST: Prod/CastMembers/Create
        // To protect from overposting attacks, enable the specific properties you want to bind to, for 
        // more details see https://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Create([Bind(Include = "CastMemberId,Name,YearJoined,MainPosition,Bio,Photo,CurrentMember,Character,CastYearLeft,DebutYearLeft")] CastMember castMember)
        {
            if (ModelState.IsValid)
            {
                db.CastMembers.Add(castMember);
                db.SaveChanges();
                return RedirectToAction("Index");
            }

            return View(castMember);
        }

        // GET: Prod/CastMembers/Edit/5
        public ActionResult Edit(int? id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
            CastMember castMember = db.CastMembers.Find(id);
            if (castMember == null)
            {
                return HttpNotFound();
            }
            return View(castMember);
        }

        // POST: Prod/CastMembers/Edit/5
        // To protect from overposting attacks, enable the specific properties you want to bind to, for 
        // more details see https://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Edit([Bind(Include = "CastMemberId,Name,YearJoined,MainPosition,Bio,Photo,CurrentMember,Character,CastYearLeft,DebutYearLeft")] CastMember castMember)
        {
            if (ModelState.IsValid)
            {
                db.Entry(castMember).State = EntityState.Modified;
                db.SaveChanges();
                return RedirectToAction("Index");
            }
            return View(castMember);
        }

        // GET: Prod/CastMembers/Delete/5
        public ActionResult Delete(int? id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
            CastMember castMember = db.CastMembers.Find(id);
            if (castMember == null)
            {
                return HttpNotFound();
            }
            return View(castMember);
        }

        // POST: Prod/CastMembers/Delete/5
        [HttpPost, ActionName("Delete")]
        [ValidateAntiForgeryToken]
        public ActionResult DeleteConfirmed(int id)
        {
            CastMember castMember = db.CastMembers.Find(id);
            db.CastMembers.Remove(castMember);
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
```
## Style Create & Edit Page
***
### CSS
```
.Prod-ProductionMember ::placeholder {
    color: var(--dark-color);
    opacity: 0.5;
}

.Prod-ProductionMember input[type="text"]:focus, .Prod-ProductionMember input[type="number"]:focus, .Prod-ProductionMember select:focus {
    outline: 0 none;
    border-color: var(--main-color--light);
    box-shadow: 0 0 0 1px var(--main-color--light);
}

.Prod-ProductionMember-createBtn {
    background-color: var(--main-color--light);
    color: var(--dark-color);
    padding: 5px 20px;
    text-align: center;
    font-size: 15px;
    font-weight: 600;
    border-radius: 8px;
}
.Prod-ProductionMember-createBtn:hover {
    background-color: var(--main-color);
    color: var(--light-color);
    border: 2px solid var(--main-color--light);
    padding: 5px 20px;
    text-align: center;
    font-size: 15px;
    font-weight: 600;
    border-radius: 8px;
    transition-duration:0.2s;
}

.Prod-ProductionMember-backBtn {
    opacity: 0.8;
    background-color: var(--dark-color);
    color: var(--light-color);
    padding: 5px 20px;
    text-align: center;
    font-size: 15px;
    font-weight: 600;
    border-radius: 8px;
    transition-duration: 0.2s;
}

.Prod-ProductionMember-backBtn:hover {
    opacity: 1;
    background-color: var(--dark-color);
    border: 2px solid var(--main-color--light);
    color: var(--main-color--light);
    padding: 5px 20px;
    text-align: center;
    font-size: 15px;
    border-radius: 8px;
}
```
### Create Page
```
<body class="cms-bg-main-light Prod-ProductionMember">
    @using (Html.BeginForm())
    {
        @Html.AntiForgeryToken()


        <div class="form-horizontal cms-bg-light cms-text-main rounded mt-5 p-3">
            <h2 class="text-center pb-2">Create Production Member</h2>
            <hr />
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            <div class="form-group row">
                @Html.LabelFor(model => model.Name, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Name, new { htmlAttributes = new { @class = "form-control", placeholder = "Name" } })
                    @Html.ValidationMessageFor(model => model.Name, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.YearJoined, "Year Joined", htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.YearJoined, new { htmlAttributes = new { @class = "form-control", placeholder = "Year Joined" } })
                    @Html.ValidationMessageFor(model => model.YearJoined, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.MainRole, "Main Role", htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EnumDropDownListFor(model => model.MainRole, htmlAttributes: new { @class = "form-control", placeholder = "Name" })
                    @Html.ValidationMessageFor(model => model.MainRole, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.Bio, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Bio, new { htmlAttributes = new { @class = "form-control", placeholder = "Bio" } })
                    @Html.ValidationMessageFor(model => model.Bio, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.CurrentMember, "Current Member", htmlAttributes: new { @class = "control-label col-md-2", placeholder = "Characteer" })
                <div class="col-md-10">
                    <div class="checkbox">
                        @Html.EditorFor(model => model.CurrentMember)
                        @Html.ValidationMessageFor(model => model.CurrentMember, "", new { @class = "text-danger" })
                    </div>
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.Character, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Character, new { htmlAttributes = new { @class = "form-control", placeholder = "Character" } })
                    @Html.ValidationMessageFor(model => model.Character, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.CastYearLeft, "Cast Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.CastYearLeft, new { htmlAttributes = new { @class = "form-control", placeholder = "Cast Year Left" } })
                    @Html.ValidationMessageFor(model => model.CastYearLeft, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row">
                @Html.LabelFor(model => model.DebutYearLeft, "Debut Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.DebutYearLeft, new { htmlAttributes = new { @class = "form-control", placeholder = "Debut Year Left" } })
                    @Html.ValidationMessageFor(model => model.DebutYearLeft, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group row text-center pt-3">
                <div class="col-md-offset-2 col-md-10">
                    <input type="submit" value="Create" class="Prod-ProductionMember-createBtn" />
                    <input type="button" class="Prod-ProductionMember-backBtn ml-5" value="Back to list" onclick="location.href='@Url.Action("Index")'" />
                </div>
            </div>
        </div>
    }
</body>
```
### Edit Page
```
<body class="cms-bg-main-light Prod-ProductionMember">
    @using (Html.BeginForm())
    {
        @Html.AntiForgeryToken()

    <div class="form-horizontal cms-bg-light cms-text-main rounded mt-5 p-3">
        <h2 class="text-center pb-2 cms-t">Edit Production Member</h2>
        <hr />
        @Html.ValidationSummary(true, "", new { @class = "text-danger" })
        @Html.HiddenFor(model => model.ProductionMemberId)

        <div class="form-group row">
            @Html.LabelFor(model => model.Name, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.Name, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.Name, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.YearJoined,"Year Joined", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.YearJoined, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.YearJoined, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.MainRole,"Main Role", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EnumDropDownListFor(model => model.MainRole, htmlAttributes: new { @class = "form-control" })
                @Html.ValidationMessageFor(model => model.MainRole, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.Bio, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.Bio, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.Bio, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.CurrentMember, "Current Member", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                <div class="checkbox">
                    @Html.EditorFor(model => model.CurrentMember)
                    @Html.ValidationMessageFor(model => model.CurrentMember, "", new { @class = "text-danger" })
                </div>
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.Character, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.Character, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.Character, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.CastYearLeft, "Cast Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.CastYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.CastYearLeft, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.DebutYearLeft, "Debut Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.DebutYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.DebutYearLeft, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row text-center pt-3">
            <div class="col-md-offset-2 col-md-10">
                <input type="submit" value="Save" class="Prod-ProductionMember-createBtn" />
                <input type="button" class="Prod-ProductionMember-backBtn ml-5" value="Back to list" onclick="location.href='@Url.Action("Index")'" />
            </div>
        </div>

    </div>
    }
</body>
```




