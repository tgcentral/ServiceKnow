var dashboard = '972a55e91b54e1102e87dc62b24bcb58'; // sys\_id of dashboard



var d = new GlideRecord('pa\_dashboards');

d.get(dashboard);

gs.info("\*\*\*\* Dashboard: " + d.name);



var reports = \[];



var grPM2DT = new GlideRecord('pa\_m2m\_dashboard\_tabs');

grPM2DT.addQuery("dashboard", dashboard);

grPM2DT.orderBy('order');

grPM2DT.query();

while (grPM2DT.next()) {



&#x20;   gs.info("\*\*\*\* Tab: " + grPM2DT.tab.getDisplayValue());

//    gs.info("   \*\*\*\* Tab.Page: " + grPM2DT.tab.page.getDisplayValue()); // sp\_portal\_page



&#x20;   var eq = 'grid\_canvas.legacy\_page=' + grPM2DT.tab.page + ''; // sp\_portal\_page

&#x20;   var grGCP = new GlideRecord('sys\_grid\_canvas\_pane');

&#x20;   grGCP.addEncodedQuery(eq);

&#x20;   grGCP.orderBy('posy');

&#x20;   grGCP.orderBy('posx');

&#x20;   grGCP.query();

&#x20;   while (grGCP.next()){



//        gs.info("       \*\*\*\* sys\_grid\_canvas\_pane: " + grGCP.getUniqueValue());



&#x20;       var grSPP = new GlideRecord("sys\_portal\_preferences");

&#x20;       grSPP.addQuery("portal\_section", grGCP.portal\_widget);

&#x09;	grSPP.addQuery("name", "renderer");

&#x20;       grSPP.query();

&#x20;       if (grSPP.next()){



&#x09;		var renderer = grSPP.getValue("value");

&#x09;		var renderReport = "com.glide.ui.portal.RenderReport";

&#x09;		

&#x09;		if (renderer == renderReport){



&#x09;			var grSPP2 = new GlideRecord("sys\_portal\_preferences");

&#x09;			grSPP2.addQuery("portal\_section", grGCP.portal\_widget);

&#x09;			grSPP2.addQuery("name", "sys\_id");

&#x09;			grSPP2.query();

&#x09;			grSPP2.next();

&#x09;			var report\_sys\_id = grSPP2.getValue("value");				



&#x20;               var grReport = new GlideRecord('sys\_report');

&#x20;               grReport.get(report\_sys\_id);



&#x20;               reports.push(report\_sys\_id);



&#x20;               gs.info("       Report: " + grReport.title + ' / ' + report\_sys\_id);

&#x09;			gs.info("           Type: " + grReport.type.getDisplayValue());

&#x09;			gs.info("           Table: " + grReport.table);

&#x09;			gs.info("           Filter: " + grReport.filter);

&#x20;               if (grReport.getValue('chart\_title'))

&#x09;			gs.info("       - Title: " + grReport.chart\_title);



&#x20;           }

&#x20;           else {

&#x09;			gs.info("       Widget: non-report widget");

&#x20;           }



&#x20;       }

&#x20;   

&#x20;   }



}



gs.info("report sys\_ids: " + reports);



// To share with group

// 1. Set sys\_report.user = 'group'

// 2. New record in sys\_report\_users\_groups



/\*

for (var i=0; i< reports.length; i++){



&#x20;   var group\_id = '2ab9828d1bf8995016a02fc7bd4bcb9d'; // N4 Purchasing

&#x20;   var gr = new GlideRecord('sys\_report\_users\_groups');

&#x20;   gr.group\_id = group\_id;

&#x20;   gr.report\_id = reports\[i]+'';

&#x20;   gr.insert();   



}\*/



/\*

var gr = new GlideRecord('sys\_report');

gr.addEncodedQuery('sys\_idIN' + reports);

gr.query();

gs.info(gr.getRowCount());

while (gr.next()){

&#x20;   gr.user = 'group';

&#x20;   gr.update();

}

\*/









// renderer

// com.glideapp.home.RenderHomepagePublishers

//      sys\_ui\_hp\_publisher

//

// com.glide.ui.portal.RenderReport

//      sys\_report

//

// com.glide.cms.RenderBlock

//      content\_block\_lists

//

// com.glide.ui.portal.RenderDashboard

//      sys\_gauge

//

// com.glide.ui.portal.RenderFilters

//      sys\_filter

//

// com.glide.ui.portal.RenderGadget

//

//

// com.glide.ui.portal.RenderJavascript

//      sys\_widgets

//

// com.glideapp.knowledge.RenderKnowledge

//      kb\_knowledge

//

// com.glide.ui.portal.RenderMenus

//      sys\_app\_application

//

// com.glideapp.servicecatalog.RenderCategory

//      sc\_category

//

// com.snc.pa.ui.RenderPerformanceAnalytics

//      pa\_widgets

//

// com.glideapp.servicecatalog.RenderCatalog

//      sc\_catalog

// 

