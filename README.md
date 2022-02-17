# C-LiveProject-TheaterCMS

<div class="container" style="font-family: Broadway">
    <div class="jumbotron mb-0" style="background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('/Content/images/theater.jpg'); background-repeat: no-repeat; background-size: cover; background-position: 50% 75%">
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
