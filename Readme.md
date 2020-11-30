##### Lesson 1: Using Layouts
##### Demonstration: How to Create a Layout and Link it to a View


Este ejemplo usa una pequeña base de datos con SQLLITE:
student.db a traves de Student.

Creamos el Modelo Student.cs.
El controlador con inyección de dependencia a StudentContext
Creamos un Layout

<pre><code>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>@ViewBag.Title</title>
    <link type="text/css" rel="stylesheet" href="~/css/style-layout-example.css" />  <!-- Añadimos el style -->
</head>
<body>
    <h1>Welcome to the University</h1> <!-- Añadimos este h1 -->
    <div>  <!-- en   @@RenderBody()  es donde se pintaran las vistas que utilicen el layout-->
         @RenderBody() 
    </div>
	 <!-- puedo tener varias    @@RenderSection() -->
    @RenderSection("footer", false)
</body>
</html>
</code></pre>

Añandimo una Vista Razor Start
<pre><code>
@{
    Layout = "_Layout";
}
</code></pre>

En el controlador creamos la vista asociada a la action INdex y la modificamos:

<pre><code>
@model IEnumerable<Student>

<h2>Students list</h2>
<div>
    <table class="table">
        <thead>
            <tr>
                <th>
                    @Html.DisplayNameFor(model => model.FirstName)
                </th>
                <th>
                    @Html.DisplayNameFor(model => model.LastName)
                </th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            @foreach (var item in Model)
            {
                <tr>
                    <td>
                        @Html.DisplayFor(modelItem => item.FirstName)
                    </td>
                    <td>
                        @Html.DisplayFor(modelItem => item.LastName)
                    </td>
                    <td>
                        <a asp-action="Details" asp-route-id="@item.StudentId">Details</a>
                    </td>
                </tr>
            }
        </tbody>
    </table>
</div>
</code></pre>

Y modificamos también al de Details:
<pre><code>
@model Student
<h2>Details</h2>

<h2>Student details</h2>

<div>
    <dl>
        <dt>
            @Html.DisplayNameFor(model => model.FirstName)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.FirstName)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.LastName)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.LastName)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.Birthdate)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.Birthdate)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.City)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.City)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.Address)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.Address)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.Course)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.Course)
        </dd>
        <dt>
            @Html.DisplayNameFor(model => model.StartedUniversityDate)
        </dt>
        <dd>
            @Html.DisplayFor(model => model.StartedUniversityDate)
        </dd>
    </dl>
</div>
@section footer {
    <div>
        <a asp-action="Index">Back to List</a>
    </div>
}
</code></pre>
