# Codelab07 - Setting up a date

We're _almost_ done! All that's left is to add the functionality to arrange a date with one of our pets. For this, we will route our app to a different component,
which means our ProfileGallery will be replaced with the SetupDate component on our screen. Let's dive into this!

## Routing to a new component

Right now, routes are not available in your application. ReactJS doesn't offer this out-of-the-box. We will have to install a library for this. Routing is an indispensable
part of every application, so this library will most likely always have to be installed. We will be using **react-router-dom** for this, which you can add to your project by typing
**npm i react-router-dom**. If you're interested in documentation on this, you can find it at [their repository](https://github.com/remix-run/react-router/blob/main/docs/getting-started/tutorial.md).

Adding routes to React is pretty straightforward. We will be adding ours in **App.jsx**. You can use the following example and adjust it to your app:
```
<div>
      <Header />
      <div className="container-fluid">
        <div className="row">
            <BrowserRouter>
                <Routes>
                  <Route exact path="/" element={<ComponentName />} />
                  <Route exact path="/path" element={<AnotherComponent />} />
                  <Route path="*" element={<Navigate to="/" />} />
                </Routes>
          </BrowserRouter>
          <Outlet />
        </div>
      </div>
      <Footer />
</div>
```

This is the code you will see in your App.jsx file after adding the routing functionality. The first two Routes are custom routes you provide to any of your components (you can pass on properties or functions to these as well). Adjust
them to show what they need to show. The first should show our ProfileGallery, the last the SetupDate component we are going to make.
The last Route is a fallback that is used whenever someone tries to go to an address that doesn't exist. It can be used to show a custom 404 page.
<Outlet /> is where the result of our routes will be shown. The component we show will be replacing <Outlet />.

Once this is done, your routes are active and working. Of course, routing to a SetupDate component won't be working since we still need to create it. Let's do that!

## Creating the SetupDate component

* Create a SetupDate component and paste the contents of setup-date.html in it.
