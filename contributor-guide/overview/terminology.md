# Terminology

While we strive as a team to use language that is inclusive to newcomers, there will inevitably be scenarios where we have to use terms that may not be immediately understood by anyone less familiar with the application. In an effort to bridge that gap, the following is a list of terms that are frequently used within the context of the OpenBoxes application:

## General Warehouse Management Terms

* LMIS: Logistics management information system. Manages the requisition, stock management, and distribution of health commodities (drugs, emergency supplies, electronics). OpenBoxes is a LMIS.
* WMS: Warehouse management system.
* HIS: Health information system.
* SOP: Standard Operating Procedure. Outlines how to perform a task efficiently.



## OpenBoxes Application-specific Terms

* OB: OpenBoxes. That's us!
* QOH: Quantity On Hand. A count of what is physically in stock
* QATP: Quantity available to pick. The Quantity On Hand that is not picked, held, or recalled
* Depot: a type of warehouse
* Inbound: Products coming into or a warehouse
* Outbound: Products going out of a warehouse
* Picking: The act of pulling an item off the shelf in a warehouse for use.
* Autopick: When we pick something in the app we need to specify the bin that we pick from. Autopick is when the app automatically decides this for you based on the QATP of each bin with that item.
* Putaway: When first receiving a shipment we’ll put the items in a temporary/virtual bin until we can properly put it away into a real bin. A put away is the action of moving stock from a virtual to a real bin.
* OBT: Ordering Template in OpenBoxes. This is the import/export tool in purchase orders.
* Bin Replenishment: Some sites have a special bulk storage that you can’t pick directly from but can use to restock your bins. Essentially this is a special type of internal stock transfer from bulk storage to a bin.
* (Internal) Stock Transfer: Moving a product internally from one bin to another.
* Transfer Order: A PDF outlining a stock transfer or bin replenishment.
* Stock Out: If a warehouse runs out of an item that is still being picked. This is bad and we’re constantly working to help sites minimize stock outs.
* Non-clinical items: Office supplies, vehicles, cleaning supplies…
* Product: Associated with a SKU. The objects that are tracked in the warehouse. A product can have multiple lots / inventory items.
* SKU: Stock Keeping Unit.
* Lot Number: A manufacturing serial number. Useful if there’s a recall, so we can process returns for all products of a given lot number.
* Inventory Item: A specific lot of a product. Should probably have been named "product lot"
* Product Code: A generated, unique id for representing a product in our system
* Stock List: A predefined list of items for regular inbound or outbound shipments. We can import a stock list when receiving new inbound shipments or sending outbound ones to allow us to auto fill the stock info.
* Stock Card: Aka bin card. A list of how much stock we have of a specific item and where it is in the warehouse (we may have an item stocked in multiple places) as well as a record of our inbound and outbound shipments of the item.
* SM: Stock Movement.
  * IM: Inbound Movement. Taking stock into the facility.
  * OM: Outbound Movement. Shipping stock out from the facility.
* PL: Packing List. A paper describing a shipment and its contents
* PO: Procurement/Purchase Order. Made when a facility orders something from a provider/vendor.
* Vendor/Supplier: A group outside the org that sends products to the warehouse.
* Substitution: When making outbound shipments, if we don’t have enough of a product to fulfill a demand, we can sometimes substitute the request with another similar product. We can also do a substitution if we find a similar product that is expiring sooner so that we don’t waste anything.
* Formulary: Coloured blue in the app. A formal way of categorizing items.
  * Global Formulary: Items we can easily order because we’ve already gone through a pre-approved sourcing process in place for them.
  * Non-Formulary: Items that are a more involved process to order
* Tags: Coloured green in the app. A less formal way of categorizing items in comparison to formularies. More for grouping items for their use case. (Ex: all items needed for graduation events at UGHE) Anyone can create tags and tag items.
* Product Family: A way of grouping similar items. (Ex: a “gloves” product family where all products that are gloves can live under).
* Bin Location: A physical space where items are stored (shelf X, fridge Y, rack Z)
  * Hold Bin: A specific type of bin whose items are placed on hold and so are unpickable (but can be returned). This could be just a way of flagging stock as unpickable, but warehouses often have an actual physical hold bin.
* Stock Count: Performing a count of the quantity of an item that you have on hand and inputting it into OpenBoxes.
* Backdating: The act of inputting stock operations (picking, receiving…) into the application a significant amount of time after they occurred in the physical warehouse.
* Encumbrance: Funds that are committed to a specific purpose. For us: an order was placed but is not shipped and/or we haven’t invoiced it yet.
* General Ledger: A big book that has one line per actual (ie order/invoice item that HAS been paid)
* GL Code: Numerical codes that represent dimensions (ie categories of items/programs/grants/activities) used in a general ledger to track what areas our funds are going to.
