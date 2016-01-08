# jquery-endless-pager
Infinite scroll for endless content visualization

Requirements
============

This plugin requires only jQuery reference

How to use
==========

The intent of this plugin is to create an endless effect applied to paginated data (grid, lists, ...).

It requires few properies:

* **nextSelector** : selector of anchor with next page link;
* **paginationSelector** : selector of container that have pagination anchors;
* **scrollContainerSelector** : selector of scrolling area container (div, popover, etc..etc..);
* **extraQueryParameters** : parameters to append to url from next page link;
* **activateOnStart** : (default: true) set if plugin should be activated at start; 

**nextSelector** and **paginationSelector** are required to work.

**extraQueryParameters** can be useful when you have multiple lists, distribuited for example in tabs. In that case you could send to server what list need next page, without load on server data for all lists.

**activateOnStart** can be useful when you have multiple lists, distribuited for example in tabs; infact if you are in the first tab and go down to bottom page, all plugins activated will make queries to server;


Example
=======

    $('#listview1').endlesspager({
    	nextSelector : '#listview1 ul.pagination li.next a',
    	paginationSelector : '#listview1 ul.pagination',
    	extraQueryParameters : 'lstview=firstListView'
    });
    
    $('#listview2').endlesspager({
    	nextSelector : '#listview2 ul.pagination li.next a',
    	paginationSelector : '#listview2 ul.pagination',
    	extraQueryParameters : 'lstview=secondListView',
    	activateOnStart : false
    });
    
    
Example using Yii2
==================
  
If you use Yii2, and the plugin is in /web/libs/endless-pager/jquery.endlesspager.js, inside the view file:

    $this->registerJsFile('@web/libs/endless-pager/jquery.endlesspager.js', ['depends' => [\yii\web\JqueryAsset::className()]]);
    $this->registerJs( <<< EOT_JS_INFINITE_SCROLL
        $('#listview1').endlesspager({
        	nextSelector : '#listview1 ul.pagination li.next a',
        	paginationSelector : '#listview1 ul.pagination',
        	extraQueryParameters : 'lstview=listview1'
        });
    EOT_JS_INFINITE_SCROLL
    );
    
    echo \yii\widgets\ListView::widget([
        'id' => 'listview1',
        'options' => ['class' => 'list-view '],
        'dataProvider' => $dataProvider,
        'layout' => '{items}{pager}',
        'itemView' => '_itemList',
    ]);
