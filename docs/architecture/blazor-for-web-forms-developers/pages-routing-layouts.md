---
title: 页面、路由和布局
description: 了解如何在 Blazor 中创建页面，使用客户端路由和管理页面布局。
author: danroth27
ms.author: daroth
ms.date: 09/19/2019
ms.openlocfilehash: 693eee270a46ccb56ed5fef8fced1d4a1cf1974f
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "73841233"
---
# <a name="pages-routing-and-layouts"></a><span data-ttu-id="a70a8-103">页面、路由和布局</span><span class="sxs-lookup"><span data-stu-id="a70a8-103">Pages, routing, and layouts</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="a70a8-104">ASP.NET Web 窗体应用由 *.aspx*文件中定义的页面组成。</span><span class="sxs-lookup"><span data-stu-id="a70a8-104">ASP.NET Web Forms apps are composed of pages defined in *.aspx* files.</span></span> <span data-ttu-id="a70a8-105">每个页面的地址基于其在项目中的物理文件路径。</span><span class="sxs-lookup"><span data-stu-id="a70a8-105">Each page's address is based on its physical file path in the project.</span></span> <span data-ttu-id="a70a8-106">当浏览器向页面发出请求时，将在服务器上动态呈现该页的内容。</span><span class="sxs-lookup"><span data-stu-id="a70a8-106">When a browser makes a request to the page, the contents of the page are dynamically rendered on the server.</span></span> <span data-ttu-id="a70a8-107">页的 HTML 标记及其服务器控件的呈现帐户。</span><span class="sxs-lookup"><span data-stu-id="a70a8-107">The rendering accounts for both the page's HTML markup and its server controls.</span></span>

<span data-ttu-id="a70a8-108">在 Blazor 中，应用中的每个页面都是一个组件，通常在*razor*文件中定义，具有一个或多个指定路由。</span><span class="sxs-lookup"><span data-stu-id="a70a8-108">In Blazor, each page in the app is a component, typically defined in a *.razor* file, with one or more specified routes.</span></span> <span data-ttu-id="a70a8-109">路由大多数发生在客户端，而不涉及特定的服务器请求。</span><span class="sxs-lookup"><span data-stu-id="a70a8-109">Routing mostly happens client-side without involving a specific server request.</span></span> <span data-ttu-id="a70a8-110">浏览器首先发出对应用程序根地址的请求。</span><span class="sxs-lookup"><span data-stu-id="a70a8-110">The browser first makes a request to the root address of the app.</span></span> <span data-ttu-id="a70a8-111">然后，Blazor 应用中的根 `Router` 组件会处理截获导航请求，并将它们处理到正确的组件。</span><span class="sxs-lookup"><span data-stu-id="a70a8-111">A root `Router` component in the Blazor app then handles intercepting navigation requests and them to the correct component.</span></span>

<span data-ttu-id="a70a8-112">Blazor 还支持*深层链接*。</span><span class="sxs-lookup"><span data-stu-id="a70a8-112">Blazor also supports *deep linking*.</span></span> <span data-ttu-id="a70a8-113">当浏览器向特定路由发出请求而不是应用的根时，将发生深层链接。</span><span class="sxs-lookup"><span data-stu-id="a70a8-113">Deep linking occurs when the browser makes a request to a specific route other than the root of the app.</span></span> <span data-ttu-id="a70a8-114">发送到服务器的深层链接请求路由到 Blazor 应用，后者随后将请求客户端路由到正确的组件。</span><span class="sxs-lookup"><span data-stu-id="a70a8-114">Requests for deep links sent to the server are routed to the Blazor app, which then routes the request client-side to the correct component.</span></span>

<span data-ttu-id="a70a8-115">ASP.NET Web 窗体中的简单页面可能包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="a70a8-115">A simple page in ASP.NET Web Forms might contain the following markup:</span></span>

<span data-ttu-id="a70a8-116">*名称 .aspx*</span><span class="sxs-lookup"><span data-stu-id="a70a8-116">*Name.aspx*</span></span>

```aspx-csharp
<%@ Page Title="Name" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Name.aspx.cs" Inherits="WebApplication1.Name" %>

<asp:Content ID="BodyContent" ContentPlaceHolderID="MainContent" runat="server">
    <div>
        What is your name?<br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
    </div>
    <div>
        <asp:Literal ID="Literal1" runat="server" />
    </div>
</asp:Content>
```

<span data-ttu-id="a70a8-117">*Name.aspx.cs*</span><span class="sxs-lookup"><span data-stu-id="a70a8-117">*Name.aspx.cs*</span></span>

```csharp
public partial class Name : System.Web.UI.Page
{
    protected void Button1_Click1(object sender, EventArgs e)
    {
        Literal1.Text = "Hello " + TextBox1.Text;
    }
}
```

<span data-ttu-id="a70a8-118">Blazor 应用中的等效页面如下所示：</span><span class="sxs-lookup"><span data-stu-id="a70a8-118">The equivalent page in a Blazor app would look like this:</span></span>

<span data-ttu-id="a70a8-119">*名称 razor*</span><span class="sxs-lookup"><span data-stu-id="a70a8-119">*Name.razor*</span></span>

```razor
@page "/Name"
@layout MainLayout

<div>
    What is your name?<br />
    <input @bind="text" />
    <button @onclick="OnClick">Submit</button>
</div>
<div>
    @if (name != null)
    {
        @:Hello @name
    }
</div>

@code {
    string text;
    string name;

    void OnClick() {
        name = text;
    }
}
```

## <a name="create-pages"></a><span data-ttu-id="a70a8-120">创建页面</span><span class="sxs-lookup"><span data-stu-id="a70a8-120">Create pages</span></span>

<span data-ttu-id="a70a8-121">若要在 Blazor 中创建页面，请创建一个组件并添加 `@page` Razor 指令，以便为该组件指定路由。</span><span class="sxs-lookup"><span data-stu-id="a70a8-121">To create a page in Blazor, create a component and add the `@page` Razor directive to specify the route for the component.</span></span> <span data-ttu-id="a70a8-122">`@page` 指令使用单个参数，该参数是要添加到该组件的路由模板。</span><span class="sxs-lookup"><span data-stu-id="a70a8-122">The `@page` directive takes a single parameter, which is the route template to add to that component.</span></span>

```razor
@page "/counter"
```

<span data-ttu-id="a70a8-123">路由模板参数是必需的。</span><span class="sxs-lookup"><span data-stu-id="a70a8-123">The route template parameter is required.</span></span> <span data-ttu-id="a70a8-124">与 ASP.NET Web 窗体不同，指向 Blazor 组件的路由*不*会从其文件位置推断出来（尽管这可能是将来添加的功能）。</span><span class="sxs-lookup"><span data-stu-id="a70a8-124">Unlike ASP.NET Web Forms, the route to a Blazor component *isn't* inferred from its file location (although that may be a feature added in the future).</span></span>

<span data-ttu-id="a70a8-125">路由模板语法是用于在 ASP.NET Web 窗体中进行路由的基本语法。</span><span class="sxs-lookup"><span data-stu-id="a70a8-125">The route template syntax is the same basic syntax used for routing in ASP.NET Web Forms.</span></span> <span data-ttu-id="a70a8-126">使用大括号在模板中指定路由参数。</span><span class="sxs-lookup"><span data-stu-id="a70a8-126">Route parameters are specified in the template using braces.</span></span> <span data-ttu-id="a70a8-127">Blazor 会将路由值绑定到具有相同名称的组件参数（不区分大小写）。</span><span class="sxs-lookup"><span data-stu-id="a70a8-127">Blazor will bind route values to component parameters with the same name (case-insensitive).</span></span>

```razor
@page "/product/{id}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public string Id { get; set; }
}
```

<span data-ttu-id="a70a8-128">您还可以对路由参数的值指定约束。</span><span class="sxs-lookup"><span data-stu-id="a70a8-128">You can also specify constraints on the value of the route parameter.</span></span> <span data-ttu-id="a70a8-129">例如，要将产品 ID 限制为 `int`：</span><span class="sxs-lookup"><span data-stu-id="a70a8-129">For example, to constrain the product ID to be an `int`:</span></span>

```razor
@page "/product/{id:int}"

<h1>Product @Id</h1>

@code {
    [Parameter]
    public int Id { get; set; }
}
```

<span data-ttu-id="a70a8-130">有关 Blazor 支持的路由约束的完整列表，请参阅[路由约束](/aspnet/core/blazor/routing#route-constraints)。</span><span class="sxs-lookup"><span data-stu-id="a70a8-130">For a full list of the route constraints supported by Blazor, see [Route constraints](/aspnet/core/blazor/routing#route-constraints).</span></span>

## <a name="router-component"></a><span data-ttu-id="a70a8-131">路由器组件</span><span class="sxs-lookup"><span data-stu-id="a70a8-131">Router component</span></span>

<span data-ttu-id="a70a8-132">Blazor 中的路由由 `Router` 组件处理。</span><span class="sxs-lookup"><span data-stu-id="a70a8-132">Routing in Blazor is handled by the `Router` component.</span></span> <span data-ttu-id="a70a8-133">`Router` 组件通常在应用程序的根组件（*app.config*）中使用。</span><span class="sxs-lookup"><span data-stu-id="a70a8-133">The `Router` component is typically used in the app's root component (*App.razor*).</span></span>

```razor
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```

<span data-ttu-id="a70a8-134">`Router` 组件将发现指定 `AppAssembly` 中和指定 `AdditionalAssemblies`中的可路由组件。</span><span class="sxs-lookup"><span data-stu-id="a70a8-134">The `Router` component discovers the routable components in the specified `AppAssembly` and in the optionally specified `AdditionalAssemblies`.</span></span> <span data-ttu-id="a70a8-135">当浏览器导航时，`Router` 会截获导航，并使用提取的 `RouteData` 呈现其 `Found` 参数的内容（如果路由与地址匹配），否则 `Router` 将呈现其 `NotFound` 参数。</span><span class="sxs-lookup"><span data-stu-id="a70a8-135">When the browser navigates, the `Router` intercepts the navigation and renders the contents of its `Found` parameter with the extracted `RouteData` if a route matches the address, otherwise the `Router` renders its `NotFound` parameter.</span></span>

<span data-ttu-id="a70a8-136">`RouteView` 组件会处理 `RouteData` 指定的匹配组件（如果有）。</span><span class="sxs-lookup"><span data-stu-id="a70a8-136">The `RouteView` component handles rendering the matched component specified by the `RouteData` with its layout if it has one.</span></span> <span data-ttu-id="a70a8-137">如果匹配的组件没有布局，则使用可选的指定 `DefaultLayout`。</span><span class="sxs-lookup"><span data-stu-id="a70a8-137">If the matched component doesn't have a layout, then the optionally specified `DefaultLayout` is used.</span></span>

<span data-ttu-id="a70a8-138">`LayoutView` 组件在指定布局中呈现其子内容。</span><span class="sxs-lookup"><span data-stu-id="a70a8-138">The `LayoutView` component renders its child content within the specified layout.</span></span> <span data-ttu-id="a70a8-139">本章稍后将详细介绍布局。</span><span class="sxs-lookup"><span data-stu-id="a70a8-139">We'll look at layouts more in detail later in this chapter.</span></span>

## <a name="navigation"></a><span data-ttu-id="a70a8-140">导航</span><span class="sxs-lookup"><span data-stu-id="a70a8-140">Navigation</span></span>

<span data-ttu-id="a70a8-141">在 ASP.NET Web 窗体中，通过将重定向响应返回到浏览器来触发到其他页面的导航。</span><span class="sxs-lookup"><span data-stu-id="a70a8-141">In ASP.NET Web Forms, you trigger navigation to a different page by returning a redirect response to the browser.</span></span> <span data-ttu-id="a70a8-142">例如：</span><span class="sxs-lookup"><span data-stu-id="a70a8-142">For example:</span></span>

```csharp
protected void NavigateButton_Click(object sender, EventArgs e)
{
    Response.Redirect("Counter");
}
```

<span data-ttu-id="a70a8-143">在 Blazor 中通常不能返回重定向响应。</span><span class="sxs-lookup"><span data-stu-id="a70a8-143">Returning a redirect response isn't typically possible in Blazor.</span></span> <span data-ttu-id="a70a8-144">Blazor 不使用请求-答复模式。</span><span class="sxs-lookup"><span data-stu-id="a70a8-144">Blazor doesn't use a request-reply model.</span></span> <span data-ttu-id="a70a8-145">不过，您可以与 JavaScript 一起直接触发浏览器导航。</span><span class="sxs-lookup"><span data-stu-id="a70a8-145">You can, however, trigger browser navigations directly, as you can with JavaScript.</span></span>

<span data-ttu-id="a70a8-146">Blazor 提供了一个 `NavigationManager` 服务，可用于：</span><span class="sxs-lookup"><span data-stu-id="a70a8-146">Blazor provides a `NavigationManager` service that can be used to:</span></span>

- <span data-ttu-id="a70a8-147">获取当前浏览器地址</span><span class="sxs-lookup"><span data-stu-id="a70a8-147">Get the current browser address</span></span>
- <span data-ttu-id="a70a8-148">获取基址</span><span class="sxs-lookup"><span data-stu-id="a70a8-148">Get the base address</span></span>
- <span data-ttu-id="a70a8-149">触发器导航</span><span class="sxs-lookup"><span data-stu-id="a70a8-149">Trigger navigations</span></span>
- <span data-ttu-id="a70a8-150">当地址更改时收到通知</span><span class="sxs-lookup"><span data-stu-id="a70a8-150">Get notified when the address changes</span></span>

<span data-ttu-id="a70a8-151">若要导航到其他地址，请使用 `NavigateTo` 方法：</span><span class="sxs-lookup"><span data-stu-id="a70a8-151">To navigate to a different address, use the `NavigateTo` method:</span></span>

```razor
@page "/"
@inject NavigationManager NavigationManager

<button @onclick="Navigate">Navigate</button>

@code {
    void Navigate() {
        NavigationManager.NavigateTo("counter");
    }
}
```

<span data-ttu-id="a70a8-152">有关所有 `NavigationManager` 成员的说明，请参阅[URI 和导航状态帮助](/aspnet/core/blazor/routing#uri-and-navigation-state-helpers)程序。</span><span class="sxs-lookup"><span data-stu-id="a70a8-152">For a description of all `NavigationManager` members, see [URI and navigation state helpers](/aspnet/core/blazor/routing#uri-and-navigation-state-helpers).</span></span>

## <a name="base-urls"></a><span data-ttu-id="a70a8-153">基 Url</span><span class="sxs-lookup"><span data-stu-id="a70a8-153">Base URLs</span></span>

<span data-ttu-id="a70a8-154">如果你的 Blazor 应用部署在基路径下，则需要使用 "路由到工作" 属性的 "`<base>`" 标记在页元数据中指定基 URL。</span><span class="sxs-lookup"><span data-stu-id="a70a8-154">If your Blazor app is deployed under a base path, then you need to specify the base URL in the page metadata using the `<base>` tag for routing to work property.</span></span> <span data-ttu-id="a70a8-155">如果应用的 "主机" 页使用 Razor 进行服务器呈现，则可以使用 `~/` 语法来指定应用程序的基址。</span><span class="sxs-lookup"><span data-stu-id="a70a8-155">If the host page for the app is server-rendered using Razor, then you can use the `~/` syntax to specify the app's base address.</span></span> <span data-ttu-id="a70a8-156">如果主机页为静态 HTML，则需要显式指定基 URL。</span><span class="sxs-lookup"><span data-stu-id="a70a8-156">If the host page is static HTML, then you need to specify the base URL explicitly.</span></span>

```html
<base href="~/" />
```

## <a name="page-layout"></a><span data-ttu-id="a70a8-157">页面布局</span><span class="sxs-lookup"><span data-stu-id="a70a8-157">Page layout</span></span>

<span data-ttu-id="a70a8-158">ASP.NET Web 窗体中的页面布局由母版页处理。</span><span class="sxs-lookup"><span data-stu-id="a70a8-158">Page layout in ASP.NET Web Forms is handled by Master Pages.</span></span> <span data-ttu-id="a70a8-159">母版页定义一个模板，其中包含一个或多个内容占位符，然后可以由各个页面提供。</span><span class="sxs-lookup"><span data-stu-id="a70a8-159">Master Pages define a template with one or more content placeholders that can then be supplied by individual pages.</span></span> <span data-ttu-id="a70a8-160">母版页在 *.master*文件中定义，并以 `<%@ Master %>` 指令开头。</span><span class="sxs-lookup"><span data-stu-id="a70a8-160">Master Pages are defined in *.master* files and start with the `<%@ Master %>` directive.</span></span> <span data-ttu-id="a70a8-161">*.Master*文件的内容会被编码为 *.aspx*页面，但添加了 `<asp:ContentPlaceHolder>` 控件来标记页面可以提供内容的位置。</span><span class="sxs-lookup"><span data-stu-id="a70a8-161">The content of the *.master* files is coded as you would an *.aspx* page, but with the addition of `<asp:ContentPlaceHolder>` controls to mark where pages can supply content.</span></span>

<span data-ttu-id="a70a8-162">*站点主*</span><span class="sxs-lookup"><span data-stu-id="a70a8-162">*Site.master*</span></span>

```aspx-csharp
<%@ Master Language="C#" AutoEventWireup="true" CodeBehind="Site.master.cs" Inherits="WebApplication1.SiteMaster" %>

<!DOCTYPE html>
<html lang="en">
<head runat="server">
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%: Page.Title %> - My ASP.NET Application</title>
    <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
</head>
<body>
    <form runat="server">
        <div class="container body-content">
            <asp:ContentPlaceHolder ID="MainContent" runat="server">
            </asp:ContentPlaceHolder>
            <hr />
            <footer>
                <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
            </footer>
        </div>
    </form>
</body>
</html>
```

<span data-ttu-id="a70a8-163">在 Blazor 中，可以使用布局组件来处理页面布局。</span><span class="sxs-lookup"><span data-stu-id="a70a8-163">In Blazor, you handle page layout using layout components.</span></span> <span data-ttu-id="a70a8-164">布局组件继承自 `LayoutComponentBase`，后者定义类型 `RenderFragment`的单个 `Body` 属性，该属性可用于呈现页面的内容。</span><span class="sxs-lookup"><span data-stu-id="a70a8-164">Layout components inherit from `LayoutComponentBase`, which defines a single `Body` property of type `RenderFragment`, which can be used to render the contents of the page.</span></span>

<span data-ttu-id="a70a8-165">*MainLayout*</span><span class="sxs-lookup"><span data-stu-id="a70a8-165">*MainLayout.razor*</span></span>

```razor
@inherits LayoutComponentBase
<h1>Main layout</h1>
<div>
    @Body
</div>
```

<span data-ttu-id="a70a8-166">呈现包含布局的页面时，页面将在指定布局的内容中呈现在布局呈现其 `Body` 属性的位置。</span><span class="sxs-lookup"><span data-stu-id="a70a8-166">When the page with a layout is rendered, the page is rendered within the contents of the specified layout at the location where the layout renders its `Body` property.</span></span>

<span data-ttu-id="a70a8-167">若要将布局应用于页面，请使用 `@layout` 指令：</span><span class="sxs-lookup"><span data-stu-id="a70a8-167">To apply a layout to a page, use the `@layout` directive:</span></span>

```razor
@layout MainLayout
```

<span data-ttu-id="a70a8-168">你可以使用 *_Imports razor*文件指定文件夹和子文件夹中的所有组件的布局。</span><span class="sxs-lookup"><span data-stu-id="a70a8-168">You can specify the layout for all components in a folder and subfolders using an *_Imports.razor* file.</span></span> <span data-ttu-id="a70a8-169">你还可以使用[路由器组件](#router-component)指定所有页面的默认布局。</span><span class="sxs-lookup"><span data-stu-id="a70a8-169">You can also specify a default layout for all your pages using the [Router component](#router-component).</span></span>

<span data-ttu-id="a70a8-170">母版页可定义多个内容占位符，但 Blazor 中的布局只有单个 `Body` 属性。</span><span class="sxs-lookup"><span data-stu-id="a70a8-170">Master Pages can define multiple content placeholders, but layouts in Blazor only have a single `Body` property.</span></span> <span data-ttu-id="a70a8-171">在未来的版本中，Blazor 布局组件的这一限制将会得到解决。</span><span class="sxs-lookup"><span data-stu-id="a70a8-171">This limitation of Blazor layout components will hopefully be addressed in a future release.</span></span>

<span data-ttu-id="a70a8-172">ASP.NET Web 窗体中的母版页可以嵌套。</span><span class="sxs-lookup"><span data-stu-id="a70a8-172">Master Pages in ASP.NET Web Forms can be nested.</span></span> <span data-ttu-id="a70a8-173">也就是说，母版页也可能使用母版页。</span><span class="sxs-lookup"><span data-stu-id="a70a8-173">That is, a Master Page may also use a Master Page.</span></span> <span data-ttu-id="a70a8-174">Blazor 中的布局组件也可能嵌套。</span><span class="sxs-lookup"><span data-stu-id="a70a8-174">Layout components in Blazor may be nested too.</span></span> <span data-ttu-id="a70a8-175">您可以将布局组件应用于布局组件。</span><span class="sxs-lookup"><span data-stu-id="a70a8-175">You can apply a layout component to a layout component.</span></span> <span data-ttu-id="a70a8-176">内部布局的内容将在外部布局中呈现。</span><span class="sxs-lookup"><span data-stu-id="a70a8-176">The contents of the inner layout will be rendered within the outer layout.</span></span>

<span data-ttu-id="a70a8-177">*ChildLayout*</span><span class="sxs-lookup"><span data-stu-id="a70a8-177">*ChildLayout.razor*</span></span>

```razor
@layout MainLayout
<h2>Child layout</h2>
<div>
    @Body
</div>
```

<span data-ttu-id="a70a8-178">*索引 razor*</span><span class="sxs-lookup"><span data-stu-id="a70a8-178">*Index.razor*</span></span>

```razor
@page "/"
@layout ChildLayout
<p>I'm in a nested layout!</p>
```

<span data-ttu-id="a70a8-179">页面呈现的输出将为：</span><span class="sxs-lookup"><span data-stu-id="a70a8-179">The rendered output for the page would then be:</span></span>

```html
<h1>Main layout</h1>
<div>
    <h2>Child layout</h2>
    <div>
        <p>I'm in a nested layout!</p>
    </div>
</div>
```

<span data-ttu-id="a70a8-180">Blazor 中的布局通常不会定义页面的根 HTML 元素（`<html>`、`<body>`、`<head>`，等等）。</span><span class="sxs-lookup"><span data-stu-id="a70a8-180">Layouts in Blazor don't typically define the root HTML elements for a page (`<html>`, `<body>`, `<head>`, and so on).</span></span> <span data-ttu-id="a70a8-181">根 HTML 元素是在 Blazor 应用程序的主机页中定义的，该页用于呈现应用程序的初始 HTML 内容（请参阅[启动 Blazor](project-structure.md#bootstrap-blazor)）。</span><span class="sxs-lookup"><span data-stu-id="a70a8-181">The root HTML elements are instead defined in a Blazor app's host page, which is used to render the initial HTML content for the app (see [Bootstrap Blazor](project-structure.md#bootstrap-blazor)).</span></span> <span data-ttu-id="a70a8-182">宿主页可以为应用程序提供多个包含周围标记的根组件。</span><span class="sxs-lookup"><span data-stu-id="a70a8-182">The host page can render multiple root components for the app with surrounding markup.</span></span>

<span data-ttu-id="a70a8-183">Blazor 中的组件（包括页面）不能 `<script>` 标记中呈现。</span><span class="sxs-lookup"><span data-stu-id="a70a8-183">Components in Blazor, including pages, can't render `<script>` tags.</span></span> <span data-ttu-id="a70a8-184">存在此呈现限制的原因是 `<script>` 标记只加载一次，因此无法更改。</span><span class="sxs-lookup"><span data-stu-id="a70a8-184">This rendering restriction exists because `<script>` tags get loaded once and then can't be changed.</span></span> <span data-ttu-id="a70a8-185">如果尝试使用 Razor 语法动态呈现标记，可能会发生意外行为。</span><span class="sxs-lookup"><span data-stu-id="a70a8-185">Unexpected behavior may occur if you try to render the tags dynamically using Razor syntax.</span></span> <span data-ttu-id="a70a8-186">相反，应将所有 `<script>` 标记添加到应用的 "主机" 页。</span><span class="sxs-lookup"><span data-stu-id="a70a8-186">Instead, all `<script>` tags should be added to the app's host page.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="a70a8-187">[上一页](components.md)
>[下一页](state-management.md)</span><span class="sxs-lookup"><span data-stu-id="a70a8-187">[Previous](components.md)
[Next](state-management.md)</span></span>