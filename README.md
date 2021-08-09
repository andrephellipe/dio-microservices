# Construindo um projeto com arquitetura baseada em microsserviços usando Spring Cloud

Projeto desenvolvido como parte do bootcamp DIO/Bolsas Santander, 
contendo uma REST API de registro de produtos, uma REST API de carrinho
de compras, um servidor de configurações, um servidor Eureka de descoberta
de serviços e um gateway centralizando as chamadas às APIs.

O projeto inicial apresentado foi baseado em versões antigas do Spring Boot,
Spring Data e Spring Cloud, exigindo adaptações para permitir o 
funcionamento com versões mais novas dessas ferramentas. 

As seguintes mudanças foram implementadas:
- Na API ``product-catalog``:
  
    - Foi removido o bean ``entityMapper`` da classe de configuração do Elasticsearch.
    O mapeamento de objetos baseado em Jackson foi removido do Spring Data 
    Elasticsearch na versão 4.0, conforme https://docs.spring.io/spring-data/elasticsearch/docs/current/reference/html/#elasticsearch.mapping.meta-model.rules.
    
    - Foi removido o atributo ``type`` da entidade ``Product``, pela mesma razão.

- Na API ``shoppingcart``:
    - Foi acrescentada ao build.gradle a dependência ``redis.clients:jedis`` necessária para o uso do
      Jedis com o Spring Data Redis
      
    - A forma de configuração do Redis apresentada também está deprecada. Foi
      utilizado um objeto ``RedisStandaloneConfiguration`` para configurar o nome
      e a porta do servidor Redis na classe ``RedisConfig``.
     
- Em todos os projetos:
    
    - Foi atualizada a propriedade ``springCloudVersion`` para 2020.0.3 nos
      arquivos build.gradle correspondentes.
      
    - Foi acrescentada a propriedade ``config:import: "configserver:"`` aos
      arquivos application.yaml correspondentes.
  
