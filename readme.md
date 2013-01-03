###jQuery.domModelr &mdash; simple DOM to Object mapping with data-* attributes.

This is a really simple way to `build` model classes in the DOM and also `populate` the DOM from a model. There are only two methods you can call: `build` and `populate`.

###Build

Using `data-model` and `data-property` tags, you can embed your model in the DOM like this:

    <fieldset id="employeeContainer" data-model="Employee">
        <div class="input">
            <span>First Name</span>
            <input type="text" data-property="FirstName" />
        </div>
        <div class="input">
            <span>Last Name</span>
            <input type="text" data-property="LastName" />
        </div>
        <div class="input">
            <span></span>
            <label for="chkFullTime">
                <input type="checkbox" data-property="IsFullTime" /> Is Full Time?
            </label>
        </div>
        <fieldset data-model="Family">
            <legend>Family</legend>
            <div class="input">
                <span>Number of Children</span>
                <input type="text" id="txtChildren" data-property="NumberOfChildren" />
            </div>
            <fieldset data-model="Pets">
                <legend>Pets</legend>
                <div class="input">
                    <span>Dog Name</span>
                    <input type="text" id="txtDogName" data-property="DogName" />
                </div>
            </fieldset>
        </fieldset>
        <button class="btnSave" rel="Employee">
            Save</button>
    </fieldset>

To extract the model, just call:

    //this will return an array of objects of all the top-level data-models it found
    var _models = $("#employeeContainer").domModelr("build");
    
    /****************************** 
    * _models[0] will simply be:
    *
    * { 
    *    FirstName: ''
    *    , LastName: ''
    *    , IsFullTime: true|false
    *    , Family: {
    *        NumberOfChildren: ''
    *        , Pets: {
    *            DogName: ''
    *        }
    *    }
    *  }
    ********************************

###Populate

You can populate a segment of the DOM with a model by calling

    //the last arg is optional - pass true to reset the form
    $("#employeeContainer").domModelr("populate", employee, *true|false*)
