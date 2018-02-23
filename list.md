Person List
====

HTML
----
    <div class="row mt-5">
        <div class="col">
            <h1 class="text-primary">Person List</h1>
            Person:
            <input id="count" type="number" min="1" max="100" value="4" />
            <button id="load" type="button" class="btn btn-success my-3 px-5">Load</button>
        </div>
    </div>
    <div class="row">
        <div class="col">
            <table class="table table-hover">
                <thead>
                <tr>
                    <th>Image</th>
                    <th>Name</th>
                    <th>City</th>
                    <th>Email</th>
                    <th>Action</th>
                </tr>
                </thead>
                <tbody id="list"></tbody>
            </table>
        </div>
    </div>

JavaScript
----
    $('#load').click((e) => {
        $('#list').empty();

        const count = $('#count').val();
        $.ajax({
            url: 'https://randomuser.me/api/?results=' + count,
            dataType: 'json',
            success: (data) => {
                console.log(data);

                data.results.forEach(p => {
                    $('#list').append(`
                        <tr>
                        <td><img src="${p.picture.thumbnail}" class="img-thumbnail" /></td>
                        <td>${p.name.title} ${p.name.first} ${p.name.last}</td>
                        <td>${p.location.city}</td>
                        <td>${p.email}</td>
                        <td>
                            <a class="btn btn-secondary btn-sm" href="detail.html?email=${p.email}"> View </a>
                        </td>
                        </tr>
                    `);
                });
            }
        });

    });
