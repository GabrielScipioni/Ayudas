# Rest Template Get()

<p align="center">
  <em>RestTemplate es una clase en el framework de Spring que permite realizar llamadas HTTP de forma sencilla en aplicaciones Java, facilitando la comunicación con servicios web. Es comúnmente utilizada para interactuar con APIs REST y realizar operaciones como obtener datos, enviar datos, actualizar recursos y eliminar recursos en un servidor remoto.</em>
</p>

### si por ejemplo tenemos un json como este:

```json
{
   "posts": [
      {
         "id": 1,
         "title": "hello"
      },
      {
         "id": 2,
         "title": "java"
      },
      {
         "id": 3,
         "title": ":V"
      }
   ],
   "profile": {
      "name": "typicode"
   }
}
```
### podriamos hacer esto para traer todos los posts
````java
@Service
public class PostRestClient {
    RestTemplate restTemplate = new RestTemplate();

    String baseResourceUrl = "url-de-nuestra-api";

    public ResponseEntity<Post[]> getPosts(){
        return restTemplate.getForEntity(baseResourceUrl, Post[].class);
    }
    public ResponseEntity<Post> getPost(Long id){
        return restTemplate.getForEntity(baseResourceUrl + "/"+ id, Post.class);
    }
}
````
### y esto si queremos traer uno solo 
````java
    public ResponseEntity<Post> getPost(Long id){
        return restTemplate.getForEntity(baseResourceUrl + "/"+ id, Post.class);
    }
````

en este caso **Post** es un Record ya que solo estamos haciendo peticiones del tipo **GET**

> [!TIP]
### de forma adicional se puede inyectar nuestro Rest Template añadiendo la [Configuracion](Config.md)

esta se veria de esta forma
````java
    @Autowired
    private RestTemplate restTemplate;
````

