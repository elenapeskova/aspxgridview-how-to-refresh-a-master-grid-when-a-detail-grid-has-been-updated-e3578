# Grid View for ASP.NET Web Forms - How to refresh a master grid on a detail grid callback
<!-- run online -->
**[[Run Online]](https://codecentral.devexpress.com/e3578/)**
<!-- run online end -->

This example demonstrates how to use the callback functionality to update the master grid when detail grid data changes.

## Overview

Handle the detail grid's client-side [BeginCallback](https://docs.devexpress.com/AspNet/js-ASPxClientGridView.BeginCallback) and [EndCallback](https://docs.devexpress.com/AspNet/js-ASPxClientGridView.EndCallback) events to refresh the master grid control when a callback is finished. Use the `command` argument property to determine the action that initiates that callback.

```aspx
<dx:ASPxGridView ID="ASPxGridView1" runat="server" KeyFieldName="Id" ... >
    <SettingsDetail ShowDetailRow="true" />
    <!-- ... -->
    <Templates>
        <DetailRow>
            <dx:ASPxGridView ID="gridProducts" runat="server" KeyFieldName="Id" ... >
                    <ClientSideEvents EndCallback="OnEndCallback" BeginCallback="OnBeginCallback" />
                <!-- ... -->
            </dx:ASPxGridView>
        </DetailRow>
    </Templates>
</dx:ASPxGridView>
```

```js
var command = "";
function OnBeginCallback(s, e) {
    command = e.command;
}
function OnEndCallback(s, e) {
    if (command == "ADDNEWROW") {
        s.Refresh();
    }
}
```

## Files to Review

* [OrderItems.cs](./CS/WebSite/App_Code/OrderItems.cs) (VB: [OrderItems.vb](./VB/WebSite/App_Code/OrderItems.vb))
* [Default.aspx](./CS/WebSite/Default.aspx) (VB: [Default.aspx](./VB/WebSite/Default.aspx))

## Documentation

* [Update a Control in a Callback of Another Control](https://docs.devexpress.com/AspNet/402219/common-concepts/callbacks/update-control-in-callback-of-another-control)
