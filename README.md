# Kendo Yii2 Adapter

It is a adapter for Yii2 that transforms Kendo Grid\`s frontend requests into ActiveQuery on backend. Supports all KendoGrid`s filtering, sorting, searching etc.

## [Kendo Grid docs](http://demos.telerik.com/kendo-ui/grid/index)

## Instalation

1. Add following line into `require` section in your `composer.json`:
```json
    "require": {
        "megapixel23/kendo-yii2-adapter": "dev-master"
    }
```
2. Add following line into `repositories` section in your `composer.json` to set up composer`s package source path:
```json
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/MEGApixel23/kendo-yii2-adapter"
        }
    ]
```

## Basic Usage

Frontend
```js
var grid = $("#grid").kendoGrid({
    dataSource: {
        type: 'json',
        transport: {
            read: '/custom/action/handler'
        },
        schema: {
            data: 'data',
            total: 'total'
        },
        pageSize: 20,
        serverPaging: true,
        serverFiltering: true
    },
    filterable: {
        mode: 'row'
    },
    pageable: true
}).data('kendoGrid');
```

Backend
```php
public function actionCustomActionHandler()
{
    if (Yii::$app->request->isAjax) {
        Yii::$app->response->format = 'json';
        $query = Items::find();
        $provider = new KendoDataProvider([
            'query' => $query
        ]);

        return [
            'data' => $provider->getModels(),
            'total' => $query->count()
        ];
    }
}
```
