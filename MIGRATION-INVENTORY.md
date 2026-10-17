Groovy idiom lint
files scanned: 3 (excluded: 0)
expression sites: 47
parse failures: 30 (site: 28, generated action script or template body: 2)
sites with a Groovy idiom, hazard or failure: 28
fancy template bodies compiled: 0
FreeMarker template locations (not compiled): 0

Idiom totals (sites, files)
 groovy
  elvis                              1     1
  map-literal                       26     1
  list-star                          1     1

Parse failures
  runtime/component/MrMarbleERP/data/MarbleErpSetupData.xml:49 moqui.entity.document.DataDocumentLink@linkUrl: expression `pagePath?:''` is Groovy (?:)
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:29 set@from: expression `orgPartyRoles*.partyId` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:56 link@parameter-map: expression `[orderType:'Sales', statusId:'OrderPlaced,OrderProcessing', statusId_op:'in']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:58 link@parameter-map: expression `[orderType:'Sales', statusId:'OrderApproved,OrderSent', statusId_op:'in']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:60 link@parameter-map: expression `[orderType:'Sales', statusId:'OrderHold']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:65 link@parameter-map: expression `[statusId:'ReqSubmitted', roleTypeId:'Customer']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:67 link@parameter-map: expression `[statusId:'ReqReviewed,ReqInProgress', statusId_op:'in', roleTypeId:'Customer']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:94 link@parameter-map: expression `[orderType:'Sales']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:101 link@parameter-map: expression `[parentShipmentType:'ShpTpOutgoing']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:121 link@parameter-map: expression `[invoiceType:'Receivable']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:126 link@parameter-map: expression `[invoiceType:'Payable',invoiceTypeEnumId:'InvoiceCreditMemo']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:144 link@parameter-map: expression `[paymentType:'Incoming',paymentTypeEnumId:'PtInvoicePayment']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:152 link@parameter-map: expression `[returnType:'Customer']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:156 link@parameter-map: expression `[shipmentTypeEnumId:'ShpTpSalesReturn']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:160 link@parameter-map: expression `[invoiceType:'Payable',invoiceTypeEnumId:'InvoiceReturn']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:164 link@parameter-map: expression `[paymentType:'Outgoing',paymentTypeEnumId:'PtRefund']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:171 link@parameter-map: expression `[roleTypeId:'OrgInternal']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:177 link@parameter-map: expression `[roleTypeId:'Employee']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:199 link@parameter-map: expression `[assetTypeEnumId:'AstTpInventory']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:257 link@parameter-map: expression `[orderType:'Purchase']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:265 link@parameter-map: expression `[parentShipmentType:'ShpTpIncoming']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:272 link@parameter-map: expression `[invoiceType:'Payable']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:277 link@parameter-map: expression `[invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceCreditMemo']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:282 link@parameter-map: expression `[paymentType:'Outgoing',paymentTypeEnumId:'PtInvoicePayment']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:289 link@parameter-map: expression `[returnType:'Supplier']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:293 link@parameter-map: expression `[shipmentTypeEnumId:'ShpTpPurchaseReturn']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:297 link@parameter-map: expression `[invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceReturn']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:301 link@parameter-map: expression `[paymentType:'Incoming',paymentTypeEnumId:'PtRefund']` is not JavaScript
  runtime/component/MrMarbleERP/screen/marble/dashboard.xml:29 set generated script is not JavaScript: Unexpected token
  runtime/component/MrMarbleERP/screen/marble.xml:72 text body: template: expression `(activeOrg.pseudoId)!` is not JavaScript

Known exclusions (not scanned)

FreeMarker

Per file (flagged sites only; before text)

runtime/component/MrMarbleERP/data/MarbleErpSetupData.xml (8 sites, 1 flagged)
  49: moqui.entity.document.DataDocumentLink@linkUrl [elvis] expression `pagePath?:''` is Groovy (?:)
      before: pagePath?:''

runtime/component/MrMarbleERP/screen/marble/dashboard.xml (38 sites, 27 flagged)
  29: set@from [list-star] expression `orgPartyRoles*.partyId` is not JavaScript
      before: orgPartyRoles*.partyId
  56: link@parameter-map [map-literal] expression `[orderType:'Sales', statusId:'OrderPlaced,OrderProcessing', statusId_op:'in']` is not JavaScript
      before: [orderType:'Sales', statusId:'OrderPlaced,OrderProcessing', statusId_op:'in']
  58: link@parameter-map [map-literal] expression `[orderType:'Sales', statusId:'OrderApproved,OrderSent', statusId_op:'in']` is not JavaScript
      before: [orderType:'Sales', statusId:'OrderApproved,OrderSent', statusId_op:'in']
  60: link@parameter-map [map-literal] expression `[orderType:'Sales', statusId:'OrderHold']` is not JavaScript
      before: [orderType:'Sales', statusId:'OrderHold']
  65: link@parameter-map [map-literal] expression `[statusId:'ReqSubmitted', roleTypeId:'Customer']` is not JavaScript
      before: [statusId:'ReqSubmitted', roleTypeId:'Customer']
  67: link@parameter-map [map-literal] expression `[statusId:'ReqReviewed,ReqInProgress', statusId_op:'in', roleTypeId:'Customer']` is not JavaScript
      before: [statusId:'ReqReviewed,ReqInProgress', statusId_op:'in', roleTypeId:'Customer']
  94: link@parameter-map [map-literal] expression `[orderType:'Sales']` is not JavaScript
      before: [orderType:'Sales']
  101: link@parameter-map [map-literal] expression `[parentShipmentType:'ShpTpOutgoing']` is not JavaScript
      before: [parentShipmentType:'ShpTpOutgoing']
  121: link@parameter-map [map-literal] expression `[invoiceType:'Receivable']` is not JavaScript
      before: [invoiceType:'Receivable']
  126: link@parameter-map [map-literal] expression `[invoiceType:'Payable',invoiceTypeEnumId:'InvoiceCreditMemo']` is not JavaScript
      before: [invoiceType:'Payable',invoiceTypeEnumId:'InvoiceCreditMemo']
  144: link@parameter-map [map-literal] expression `[paymentType:'Incoming',paymentTypeEnumId:'PtInvoicePayment']` is not JavaScript
      before: [paymentType:'Incoming',paymentTypeEnumId:'PtInvoicePayment']
  152: link@parameter-map [map-literal] expression `[returnType:'Customer']` is not JavaScript
      before: [returnType:'Customer']
  156: link@parameter-map [map-literal] expression `[shipmentTypeEnumId:'ShpTpSalesReturn']` is not JavaScript
      before: [shipmentTypeEnumId:'ShpTpSalesReturn']
  160: link@parameter-map [map-literal] expression `[invoiceType:'Payable',invoiceTypeEnumId:'InvoiceReturn']` is not JavaScript
      before: [invoiceType:'Payable',invoiceTypeEnumId:'InvoiceReturn']
  164: link@parameter-map [map-literal] expression `[paymentType:'Outgoing',paymentTypeEnumId:'PtRefund']` is not JavaScript
      before: [paymentType:'Outgoing',paymentTypeEnumId:'PtRefund']
  171: link@parameter-map [map-literal] expression `[roleTypeId:'OrgInternal']` is not JavaScript
      before: [roleTypeId:'OrgInternal']
  177: link@parameter-map [map-literal] expression `[roleTypeId:'Employee']` is not JavaScript
      before: [roleTypeId:'Employee']
  199: link@parameter-map [map-literal] expression `[assetTypeEnumId:'AstTpInventory']` is not JavaScript
      before: [assetTypeEnumId:'AstTpInventory']
  257: link@parameter-map [map-literal] expression `[orderType:'Purchase']` is not JavaScript
      before: [orderType:'Purchase']
  265: link@parameter-map [map-literal] expression `[parentShipmentType:'ShpTpIncoming']` is not JavaScript
      before: [parentShipmentType:'ShpTpIncoming']
  272: link@parameter-map [map-literal] expression `[invoiceType:'Payable']` is not JavaScript
      before: [invoiceType:'Payable']
  277: link@parameter-map [map-literal] expression `[invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceCreditMemo']` is not JavaScript
      before: [invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceCreditMemo']
  282: link@parameter-map [map-literal] expression `[paymentType:'Outgoing',paymentTypeEnumId:'PtInvoicePayment']` is not JavaScript
      before: [paymentType:'Outgoing',paymentTypeEnumId:'PtInvoicePayment']
  289: link@parameter-map [map-literal] expression `[returnType:'Supplier']` is not JavaScript
      before: [returnType:'Supplier']
  293: link@parameter-map [map-literal] expression `[shipmentTypeEnumId:'ShpTpPurchaseReturn']` is not JavaScript
      before: [shipmentTypeEnumId:'ShpTpPurchaseReturn']
  297: link@parameter-map [map-literal] expression `[invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceReturn']` is not JavaScript
      before: [invoiceType:'Receivable',invoiceTypeEnumId:'InvoiceReturn']
  301: link@parameter-map [map-literal] expression `[paymentType:'Incoming',paymentTypeEnumId:'PtRefund']` is not JavaScript
      before: [paymentType:'Incoming',paymentTypeEnumId:'PtRefund']
