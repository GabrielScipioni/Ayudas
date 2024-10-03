# Config

<p align="center">
  <em>Esta configuración en Spring Boot crea una instancia de RestTemplate que estará disponible para inyección en cualquier parte de tu aplicación, lo que facilita realizar llamadas HTTP a servicios externos.</em>
</p>

### Ejemplo

```java
@Configuration
public class RestTemplateConfig {

    @Bean
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }
}
```

#### de esta forma nuestra aplicacion nos dejara hacer ``@Autowired`` en nuestro Rest Template
