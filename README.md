A framework to move from zero to big  

```php 
//call web service api by autoloading namespace approach
$api = APIFactory::getAPI(LocalAPI::class);
$responseByLocal = $api->get(url('api/news'), [
    '_fields' => 'id,title,summary,content,media,comment_count,like_count,dislike_count,view_count,create_at',
    '_limit' => 5,
    '_include' => json_encode([
        'author' => [
            '_fields' => 'id,name,avatar',
            '_limit' => 1
        ],
        'comments' => [
            '_fields' => 'id,content,create_at,reply_count',
            '_include' => json_encode([
                'author' => [
                    '_fields' => 'id,name,avatar',
                    '_limit' => 5,
                ]
            ])
        ]
    ])
]);

//call web service api with cURL or something that make real request
$api = APIFactory::getAPI(RemoteAPI::class);
$responseByRemote = $api->get(url('api/news'), [
    '_fields' => 'id,title,summary,content,media,comment_count,like_count,dislike_count,view_count,create_at',
    '_limit' => 5,
    '_include' => json_encode([
        'author' => [
            '_fields' => 'id,name,avatar',
            '_limit' => 1
        ],
        'comments' => [
            '_fields' => 'id,content,create_at,reply_count',
            '_include' => json_encode([
                'author' => [
                    '_fields' => 'id,name,avatar',
                    '_limit' => 5,
                ]
            ])
        ]
    ])
]);

assertEquals($responseByLocal, $responseByRemote);
 ```
