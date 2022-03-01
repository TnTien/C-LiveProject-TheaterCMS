# C-LiveProject-TheaterCMS
## Introduction
For two weeks I was working with a team to built an interactive website for managing the content and productions for a theater/acting company. The application is built using ASP.NET MVC and Entity Framework. I was tasked with styling the Donate Page and also creating and styling the CRUD Pages for Production Members. To keep track of the progress of each member, the Agile metholody is used. We had daily standups to talk about what we did the day before and what we are planning on working the day of and also if we have any roadblocks. At the end of the week we had a Code retrospective to talk about how well the project is going and what we could to improve or what we liked.

## Create and Style Donation Page

Using Bootstrap 4, I was able to create a form that collapses into a single column as the the size of the screen decreases. The client wanted to have an image behind the title and I was able to make happen with bootstrap's jumbotron.

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
I was tasked to create the CRUD Page in order for the client to easily manage their data. Utilzing ASP.NET MVC and Entity Framework, I was able to create an entity model using Code First so that the client can save data to the database. Afterwards I was able to scaffold the model to create the CRUD pages.
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

## Style CRUD Pages
The next task I was given was to style the CRUD Pages. The client had a color theme that was to be used for styling the pages and I was provided a rough layout of how each page should look like, but ultimately it was up to me to style the page.
***
### CSS
These were the custom css that I made to style the pages. These were used to style the content of the pages.
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

.Prod-ProductionMember-IndexContainer {
    background-color: var(--secondary-color);
    padding: 0;
    overflow: hidden;
    max-width: 350px;
    margin: 5px;
    border-color: var(--light-color);
    box-shadow: 0 0 0 1px var(--main-color--light);
}

.Prod-ProductionMember-IndexContainer article {
    padding: 10%;
    position: absolute;
    bottom: 0;
    z-index: 1;
    -webkit-transition: all 0.5s ease;
    -moz-transition: all 0.5s ease;
    -o-transition: all 0.5s ease;
    -ms-transition: all 0.5s ease;
    transition: all 0.5s ease;
}

.Prod-ProductionMember-IndexContainer h2 {
    color: var(--light-color);
    font-weight: 800;
    font-size: 25px;
    border-bottom: #fff solid 1px;
}

.Prod-ProductionMember-IndexContainer h4 {
    font-weight: 300;
    color: var(--light-color);
    font-size: 16px;
}

.Prod-ProductionMember-IndexContainer img {
    width: 100%;
    top: 0;
    left: 0;
    opacity: 0.8;
    -webkit-transition: all 4s ease;
    -moz-transition: all 4s ease;
    -o-transition: all 4s ease;
    -ms-transition: all 4s ease;
    transition: all 4s ease;
}

.Prod-ProductionMember-ImgHover {
    background-color: var(--secondary-color);
    position: absolute;
    width: 100%;
    height: 60px;
    bottom: 0;
    z-index: 1;
    opacity: 0;
    transform: translate(0px, 60px);
    -webkit-transform: translate(0px, 60px);
    -moz-transform: translate(0px, 60px);
    -o-transform: translate(0px, 60px);
    -ms-transform: translate(0px, 60px);
    -webkit-transition: all 0.2s ease-in-out;
    -moz-transition: all 0.2s ease-in-out;
    -o-transition: all 0.2s ease-in-out;
    -ms-transition: all 0.2s ease-in-out;
    transition: all 0.2s ease-in-out;
}

.Prod-ProductionMember-ImgHover span {
    font-size: 40px;
    color: var(--dark-color);
    position: relative;
    margin: 0 auto;
    width: 100%;
    top: 13px;
}

/* ProductionMembers Index Page: Hover*/
.Prod-ProductionMember-IndexContainer:hover {
    cursor: pointer;
}

.Prod-ProductionMember-IndexContainer:hover img {
    opacity: 0.5;
    transform: scale(1.2);
}

.Prod-ProductionMember-IndexContainer:hover article {
    transform: translate(2px, -69px);
    -webkit-transform: translate(2px, -69px);
    -moz-transform: translate(2px, -69px);
    -o-transform: translate(2px, -69px);
    -ms-transform: translate(2px, -69px);
}

.Prod-ProductionMember-IndexContainer:hover .Prod-ProductionMember-ImgHover {
    transform: translate(0px, 0px);
    -webkit-transform: translate(0px, 0px);
    -moz-transform: translate(0px, 0px);
    -o-transform: translate(0px, 0px);
    -ms-transform: translate(0px, 0px);
    opacity: 1;
}
.Prod-ProductionMember-Index {
    border-color: var(--main-color);
    box-shadow: 0 0 0 1px var(--main-color--light);
    padding: 12px;
    border-radius: .5rem;
    box-shadow: 2px 2px 38px var(--main-color--light) inset;
    border: 5px inset var(--main-color); 
}
```

### Create Page
For the Create page, I made it so it was similar to the Donate Page earlier where I have two columns, one columns display the Name of the columns and the second with an input for the user to enter the data. As the size of the screen decreases, the form will collapse into one column. 
```
<body class="cms-bg-main-light Prod-ProductionMember">

    @using (Html.BeginForm("Create", "ProductionMembers", FormMethod.Post, new { enctype = "multipart/form-data" }))
    {
        @Html.AntiForgeryToken()

    <div class="form-horizontal cms-bg-light cms-text-main rounded mt-5 p-3">
        <h2 class="text-center pb-2">Create Production Member</h2>
        <hr />
        @Html.ValidationSummary(true, "", new { @class = "text-danger" })

        <div class="form-group row">
            @Html.LabelFor(model => model.ProductionTitle, "Production Title", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.ProductionTitle, new { htmlAttributes = new { @class = "form-control", placeholder = "Name" } })
                @Html.ValidationMessageFor(model => model.ProductionTitle, "", new { @class = "text-danger" })
            </div>
        </div>

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
            @Html.LabelFor(model => model.CurrentMember, "Current Member", htmlAttributes: new { @class = "control-label col-md-2", placeholder = "Character" })
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

        <div class="form-group row">
            @Html.LabelFor(model => model.Photo, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                <input type="file" name="imgFile" />
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
The Edit page was styled similar to the Create page. The one difference with the Edit page is that I had the page display an image if there were one. I added a feature to this page where the user would be able to remove the image but still remain on this page.
```
<body class="cms-bg-main-light Prod-ProductionMember">
    @using (Html.BeginForm("Edit", "ProductionMembers", FormMethod.Post, new { enctype = "multipart/form-data" }))
    {
        @Html.AntiForgeryToken()

    <div class="form-horizontal cms-bg-light cms-text-main rounded mt-5 p-3">
        <h2 class="text-center pb-2 cms-t">Edit Production Member</h2>
        <hr />
        @Html.ValidationSummary(true, "", new { @class = "text-danger" })
        @Html.HiddenFor(model => model.ProductionMemberId)

        <div class="form-group row">
            @Html.LabelFor(model => model.ProductionTitle, "Production Title", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.ProductionTitle, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.ProductionTitle, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.Name, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.Name, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.Name, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.YearJoined, "Year Joined", htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @Html.EditorFor(model => model.YearJoined, new { htmlAttributes = new { @class = "form-control" } })
                @Html.ValidationMessageFor(model => model.YearJoined, "", new { @class = "text-danger" })
            </div>
        </div>

        <div class="form-group row">
            @Html.LabelFor(model => model.MainRole, "Main Role", htmlAttributes: new { @class = "control-label col-md-2" })
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

        <div class="form-group row">
            @Html.LabelFor(model => model.Photo, htmlAttributes: new { @class = "control-label col-md-2" })
            <div class="col-md-10">
                @{
                    if (Model.Photo == null)
                    {
                        <p>No Photo</p>
                        <input type="file" name="imgFile" />
                    }
                    else
                    {
                        <img class="Prod-ProductionMember-Img" src="@Url.Action("DisplayImg","ProductionMembers",new { Model.ProductionMemberId })" />
                        <input type="submit" value="Remove" name="Remove" />
                        <div>
                            <div class="col">
                                <p>Replace File:</p>
                            </div>
                            <div class="col">
                                <input type="file" name="imgFile" />
                            </div>
                        </div>
                    }
                }
            </div>
        </div>

        <div class="form-group row text-center pt-3">
            <div class="col-md-offset-2 col-md-10">
                <input type="submit" value="Save" class="Prod-ProductionMember-createBtn" name="Save" />
                <input type="button" class="Prod-ProductionMember-backBtn ml-5" value="Back to list" onclick="location.href='@Url.Action("Index")'" />
            </div>
        </div>

    </div>
    }
</body>
```

## Photo Storage & Retrieval
The next step was to be able to upload an image file and save it to the database and also to be able to retrieve the image file form the data base and display it on the page. This was not an easy task. To be able to save the image to the database I had to convert the image into a byte[] and then to retrieve that I had to retrieve the byte[] and convert it back into the image file. Luckily with Entity Framework, I was able to access the database to create, edit, and delete with just a few lines.
### Controller
```
        // Retrieves uploaded img file and converts into byte[]
        public byte[] ImgtoByte(HttpPostedFileBase imgFile)
        {
            byte[] bytes;
            using (BinaryReader br = new BinaryReader(imgFile.InputStream))
            {
                bytes = br.ReadBytes(imgFile.ContentLength);
            }
            return bytes;
        }

        // Retrieves img file from db and displays img
        public ActionResult DisplayImg(ProductionMember id)
        {
            ProductionMember member = db.ProductionMembers.Find(id.ProductionMemberId);
            byte[] img = member.Photo;
                if (img != null)
                {
                    return File(img, "image/png");
                }
                else return null;
        }

        // Removes img from database on Edit page
        public ProductionMember RemoveImage(ProductionMember productionMember)
        {
            ProductionMember member = db.ProductionMembers.Find(productionMember.ProductionMemberId);
            if (member == null)
            {
                return null;
            }
            else
            {
                if (ModelState.IsValid)
                {
                    member.Photo = null;
                    db.Entry(member).State = EntityState.Modified;
                    db.SaveChanges();
                    return productionMember;
                }
            }
            return productionMember;
        }
```
I ran into some issues with the Edit page. When I went into the Edit page to change the data on some of the field but not the image, when I saved the form, the form would send the current form with an empty image because no image file was uploaded on the input for the image. In order to prevent that from happening, I created a TempData to capture the current data before the new form is submitted on the Edit page. Afterwards, I would compare the TempData with the Data that was updated. If the previous form had and image but the updated form had a null value for the image file, then the image from the TempData would be used.
```
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Create([Bind(Include = "ProductionMemberId,Name,YearJoined,MainRole,Bio,CurrentMember,Character,CastYearLeft,DebutYearLeft,ProductionTitle")] ProductionMember productionMember, HttpPostedFileBase imgFile)
        {
            if (ModelState.IsValid)
            {
                if (imgFile != null)
                {
                    db.ProductionMembers.Add(productionMember);
                    productionMember.Photo = ImgtoByte(imgFile);
                }
                else
                {
                    db.ProductionMembers.Add(productionMember);
                }
                db.SaveChanges();
                return RedirectToAction("Index");
            }

            return View(productionMember);
        }

        // GET: Prod/ProductionMembers/Edit/5
        public ActionResult Edit(int? id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
            ProductionMember productionMember = db.ProductionMembers.Find(id);
            if (productionMember == null)
            {
                return HttpNotFound();
            }
            //  TempData to pass value to a different method
            TempData["previousMember"] = productionMember;
            return View(productionMember);
        }

        // POST: Prod/ProductionMembers/Edit/5
        // To protect from overposting attacks, enable the specific properties you want to bind to, for 
        // more details see https://go.microsoft.com/fwlink/?LinkId=317598.
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Edit([Bind(Include = "ProductionMemberId,Name,YearJoined,MainRole,Bio,CurrentMember,Character,CastYearLeft,DebutYearLeft,ProductionTitle")] ProductionMember productionMember, HttpPostedFileBase imgFile)
        {
            if (ModelState.IsValid)
            {
                if (Request.Form["Save"] != null)
                {                
                    //  Retrieves TempData
                    ProductionMember previousMember = TempData["previousMember"] == null ? db.ProductionMembers.Find(productionMember.ProductionMemberId) :
                       (ProductionMember)TempData["previousMember"];
                    if (imgFile != null)
                    {
                        productionMember.Photo = ImgtoByte(imgFile);
                    }
                    //  If no file is uploaded but productionMember has a photo, this ensures that the productionMember.Photo is kept instead of changing to a null value.
                    if (imgFile == null && productionMember.Photo == null && previousMember.Photo != null)
                    {
                        productionMember.Photo = previousMember.Photo;
                    }
                    db.Entry(productionMember).State = EntityState.Modified;
                    db.SaveChanges();
                    return RedirectToAction("Index");
                }
                else if (Request.Form["Remove"] != null)
                {
                    RemoveImage(productionMember);
                    return RedirectToAction("Edit", new { id = productionMember.ProductionMemberId });
                }

            }
            return View(productionMember);
        }
```

## Index Page Styling
For the Index page. I had to change it so that it would display the Production Members based on the Production that they were in. Each member would be displayed as a card where if you click on the card you would get directed to the Details page. When you hover over the card, an overlay would appear with buttons to the Edit page and the Delete page while the image would slightly get darker. Using Razor Syntax, I first sorted the model by the ProductionTitle and only had the first displayed as a header for the Row that way there wouldn't be multiple rows of the same ProductionTitle. Next I displayed the Production Members under the Production Title that they were in. If they were not in any Production, they would be listed last.
```
<head>
    <script src="https://kit.fontawesome.com/634caf7d3f.js" crossorigin="anonymous"></script>
</head>
<div class="text-center m-3">
    <h2 class="cms-text-light">Production Members</h2>
    <button class="Prod-ProductionMember-createBtn text-center" type="button" onclick="location.href='@Url.Action("Create")'">Create</button>
</div>

<div class="container-fluid cms-bg-main-light text-center rounded Prod-ProductionMember-Index">

    @foreach (var name in Model.GroupBy(x => x.ProductionTitle).Select(y => y.First()).ToList())
    {
        if (name.ProductionTitle == null)
        {
            <h2 class="CMS-text-bigger cms-text-dark">No Production</h2>
        }
        <h2 class="CMS-text-bigger cms-text-dark">@Html.DisplayFor(modelName => name.ProductionTitle)</h2>
        <hr />
        <div class="row">

            @foreach (var item in Model)
            {
                if (item.ProductionTitle == name.ProductionTitle)
                {
                    <div class="col-3">
                        <div class="Prod-ProductionMember-IndexContainer card">
                            <div class="Prod-ProductionMember-ImgHover text-center">
                                <button class="Prod-ProductionMember-createBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Edit", "ProductionMembers", new {id = item.ProductionMemberId })'"><i class="fa-solid fa-pen-to-square"></i> Edit</button>
                                <button class="Prod-ProductionMember-backBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Delete", "ProductionMembers", new {id = item.ProductionMemberId })'"><i class="fa-solid fa-trash"></i> Delete</button>
                            </div>
                            <a href="@Url.Action("Details",new { id = item.ProductionMemberId })">
                                <article class="text-left">
                                    <h2>@Html.DisplayFor(modelItem => item.Name)</h2>
                                    <h4>@Html.DisplayFor(modelItem => item.Character)</h4>
                                </article>
                                <img src="@Url.Action("DisplayImg", "ProductionMembers", new { item.ProductionMemberId })" class="Prod-ProductionMember-imgsize" alt="">
                            </a>
                        </div>

                    </div>
                }
            }
        </div>
    }
</div>
```
### Controller
Null values of ProductionTitle would get sorted first, in order for me to have it last, before sending the Table to the Index view, I had it sorted so that Null value is last.
```
        public ActionResult Index()
        {
            var productionTitle = db.ProductionMembers.OrderBy(x => x.ProductionTitle == null)
                .ThenBy(x => x.ProductionTitle)
                .ThenBy(x => x.Name == null)
                .ThenBy(x => x.Name);
            return View(productionTitle.ToList());
        }
```
## Details & Delete Page Styling
The last task was to style the Details and Delete Pages. I was given an overview of how I could style the page so I styled the pages based on it. For the information on the second box, I made it so that it had two columns that collapses into one when the screen size is smaller.
### Details
```
<head>
    <script src="https://kit.fontawesome.com/634caf7d3f.js" crossorigin="anonymous"></script>
</head>
<body>
    <h2 class="text-center m-4">Details</h2>

    <div class="container-fluid cms-bg-main-light text-center rounded Prod-ProductionMember-Index cms-text-dark">

        <div class="text-center">
            <h2 class="text-center">@Html.DisplayFor(modelItem => Model.Name)</h2>
        </div>


        <div class="text-center">
            <div>
                @{
                    if (Model.Photo == null)
                    {
                        <p>No Photo</p>
                    }
                    else
                    {
                        <img class="mb-3 Prod-ProductionMember-Img" src="@Url.Action("DisplayImg","ProductionMembers",new { Model.ProductionMemberId })" />
                    }
                }
            </div>
        </div>
        <p class="text-left h2 row ml-1">Bio</p>
        <div class="cms-bg-light rounded Prod-ProductionMember-Index mb-2 row ml-1 mr-1 justify-content-center">
            <p>@Html.DisplayFor(modelItem => Model.Bio)</p>
        </div>

        <div class="container text-center cms-bg-light rounded Prod-ProductionMember-Index mt-2">
            <div class=" form-horizontal">
                <div class="form-group row">
                    @Html.LabelFor(model => model.ProductionTitle, "Production Title", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.ProductionTitle, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.Character, "Character", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.Character, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.YearJoined, "Year Joined", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.YearJoined, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.CastYearLeft, "Cast Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.CastYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.DebutYearLeft, "Debut Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.DebutYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
            </div>
        </div>



    </div>

    <button class="Prod-ProductionMember-backBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Index")'"><i class="fa-solid fa-backward"></i> Back to List</button>
    <button class="Prod-ProductionMember-createBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Edit", "ProductionMembers", new {id = Model.ProductionMemberId })'"><i class="fa-solid fa-pen-to-square"></i> Edit</button>
    
</body>
```
### Delete
```
<head>
    <script src="https://kit.fontawesome.com/634caf7d3f.js" crossorigin="anonymous"></script>
</head>
<body>

    <h2 class="text-center m-5">Delete this Production Member?</h2>

    <div class="container-fluid cms-bg-main-light text-center rounded Prod-ProductionMember-Index cms-text-dark">

        <div class="text-center">
            <h2 class="text-center">@Html.DisplayFor(modelItem => Model.Name)</h2>
        </div>


        <div class="text-center">
            <div>
                @{
                    if (Model.Photo == null)
                    {
                        <p>No Photo</p>
                    }
                    else
                    {
                        <img class="mb-3 Prod-ProductionMember-Img" src="@Url.Action("DisplayImg","ProductionMembers",new { Model.ProductionMemberId })" />
                    }
                }
            </div>
        </div>
        <p class="text-left h2 row ml-1">Bio</p>
        <div class="cms-bg-light rounded Prod-ProductionMember-Index mb-2 row ml-1 mr-1 justify-content-center">
            <p>@Html.DisplayFor(modelItem => Model.Bio)</p>
        </div>

        <div class="container text-center cms-bg-light rounded Prod-ProductionMember-Index mt-2">
            <div class=" form-horizontal">
                <div class="form-group row">
                    @Html.LabelFor(model => model.ProductionTitle, "Production Title", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.ProductionTitle, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.Character, "Character", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.Character, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.YearJoined, "Year Joined", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.YearJoined, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.CastYearLeft, "Cast Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.CastYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
                <div class="form-group row">
                    @Html.LabelFor(model => model.DebutYearLeft, "Debut Year Left", htmlAttributes: new { @class = "control-label col-md-2" })
                    <div class="col">
                        @Html.DisplayFor(model => model.DebutYearLeft, new { htmlAttributes = new { @class = "form-control" } })
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="container">
        <div class="row justify-content-between">
        <div>
            <button class="Prod-ProductionMember-backBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Index")'"><i class="fa-solid fa-backward"></i> Back to List</button>
            <button class="Prod-ProductionMember-createBtn text-center mt-2" type="button" onclick="location.href='@Url.Action("Edit", "ProductionMembers", new {id = Model.ProductionMemberId })'"><i class="fa-solid fa-pen-to-square"></i> Edit</button>
        </div>
        <div>
            @using (Html.BeginForm())
            {
                @Html.AntiForgeryToken()
                <button class="Prod-ProductionMember-backBtn text-center mt-2" type="submit" value="Delete" onclick="@Url.Action("DeleteConfirmed", "ProductionMembers", new { id = Model.ProductionMemberId })"><i class="fa-solid fa-trash"></i> Delete</button>
            }
        </div>
        </div>
    </div>
</body>
```
### Summary
This was a fun two weeks where I was able to put together everthing that I have learned during my time with the boot camp. With a team working on a project, it could get hectic with everyone working on the code but with the use of version control, all the changes are tracked and one person is in charge of what changes gets pushed into the main branch. I learned the importance of keeping my branch up to date with the master branch so that there aren't any merge conflicts. I think the most important thing I learned from this project is the importance of debugging. There were times when I couldn't figure out what I needed to do, so I didn't know what I needed to search to help find an answer. When I used the debugger it helped me see what my code is doing and from there I was able to narrow down what I needed to find.




