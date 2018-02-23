Person Detail
====

HTML
----
    <div class="row mt-5">
        <div class="col"><h1>Details</h1></div>
    </div>
    <div class="d-flex justify-content-center">
        <div style="width: 300px;">
            <div class="text-center">
                <img id="avatar" src="" class="img-fluid rounded-circle">
            </div>
            <p id="name" class="lead font-weight-bold text-center"></p>
            <div class="row">
                <div class="col-2">Email:</div>
                <div id="email" class="col"></div>
            </div>
            <div class="row">
                <div class="col-2">Phone:</div>
                <div id="phone" class="col"></div>
            </div>
            <div class="row">
                <div class="col-2">Address:</div>
                <div id="address" class="col"></div>
            </div>
            <div class="row">
                <div class="col-2">Account:</div>
                <div id="account" class="col"></div>
            </div>
        </div>
    </div>


JavaScript
----
    function params() {
        return location.search.substr(1).split('&').reduce((params, param) => {
            const pair = param.split('=');
            params[pair[0]] = pair[1];
            return params;
        }, {});
    }

    console.info('email', params().email);
    $.ajax({
        url: 'https://randomuser.me/api/?seed=' + (params().email || 'anybody'),
        dataType: 'json',
        success: (data) => {
            console.log(data);
            const person = data.results[0];
            $('#avatar').attr('src', person.picture.large);
            $('#name').append(`${person.name.title} ${person.name.first} ${person.name.last} `);
            $('#email').append(`${person.email}`);
            $('#phone').append(`${person.phone}`);
            $('#address').append(`${person.location.street}<br/>${person.location.postcode} ${person.location.city}<br/>${person.location.state} (${person.nat})`);
            $('#account').append(`${person.login.username}<br/>(since ${person.registered})`);
        }
    });
