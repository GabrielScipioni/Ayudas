# Test

<p align="center">
  <em>Los test son lo mas importante. ya lo abordamos en el capitulo de tets pero aca te mostramos como testear de forma Integrada o de forma unitaria a los REST Template</em> 
</p>

siguiendo con los ejemplos de Post y Profile mostraremos estos ``test``

## Unitarios

````java
@SpringBootTest
class PostRestClientTest {

    @MockBean
    private RestTemplate restTemplate;

    @SpyBean
    private PostRestClient postRestClient;

    @Test
    void getPostsTest(){
        Post post1 = new Post(1L, "test 1");
        Post post2 = new Post(2L, "test 2");
        Post[] arrayPost = {post1,post2};
        when(restTemplate.getForEntity("https://my-json-server.typicode.com/GabrielScipioni/fake-api/posts",Post[].class))
                .thenReturn(ResponseEntity.ok(arrayPost));
        ResponseEntity<Post[]> result = postRestClient.getPosts();
        assertEquals(2, Objects.requireNonNull(result.getBody()).length);
        assertEquals("test 1", Objects.requireNonNull(result.getBody())[0].title());
        assertEquals("test 2", Objects.requireNonNull(result.getBody())[1].title());
    }
    @Test
    void getPostTest(){
        Post post1 = new Post(1L, "test 1");
        when(restTemplate.getForEntity("https://my-json-server.typicode.com/GabrielScipioni/fake-api/posts/1",Post.class))
                .thenReturn(ResponseEntity.ok(post1));
        ResponseEntity<Post> result = postRestClient.getPost(1L);

        assertEquals("test 1", Objects.requireNonNull(result.getBody()).title());
    }
}
````
## Integracion

````java
@SpringBootTest
class PostRestClientIT {

    @Autowired
    private PostRestClient postRestClient;

    @Test
    void getPostsIntegrationTest() {
        ResponseEntity<Post[]> result = postRestClient.getPosts();
        assertEquals(3, Objects.requireNonNull(result.getBody()).length);
    }

    @Test
    void getPostIntegrationTest() {
        ResponseEntity<Post> result = postRestClient.getPost(1L);
        assertEquals("hello", Objects.requireNonNull(result.getBody()).title());
    }
}
````