## 理解OAuth2
### 授权类型
* authorization code
* implicit
* resource owner password credentials
* client credentials
* 自定义扩展类型


## oauth tags
### authorization-server
生成一个org.springframework.security.oauth2.provider.endpoint.AuthorizationEndpoint。
* 属性
    * client-details-service-ref
    * token-services-ref
    * user-approval-handler-ref
    * approval-parameter-name
    * authorization-endpoint-url
    * authorization-request-manager-ref
    * error-page
    * redirect-resolver-ref
    * token-endpoint-url
    * token-granter-ref ： 一个TokenGranter，默认是：CompositeTokenGranter
    * user-approval-page
* 子元素
    * authorization-code:生成AuthorizationCodeTokenGranter
        * disabled
        * authorization-code-services-ref：默认为InMemoryAuthorizationCodeServices
        * client-token-cache-ref

### resource-server
### client-details-service
### client
### resource
### rest-template
### expression-handle
### web-expression-handler