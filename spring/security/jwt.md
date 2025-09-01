# JWT

## Dependency
```gradle
implementation("org.springframework.boot:spring-boot-starter-oauth2-resource-server")
```

## JWT decoding with Nimbus
JWT decoder setup with secret:
```java
@Bean
public JwtDecoder jwtDecoder() {
    return NimbusJwtDecoder
        .withSecretKey(new SecretKeySpec(jwtSecret.getBytes(), "HmacSHA256"))
        .build();
}
```
JWT decoder setup with jwk set uri (e.g. for oauth with Google)
```java
@Bean
public JwtDecoder jwtDecoder() {
    return NimbusJwtDecoder.withJwkSetUri(jwkSetUri).build();
}
```
Decoding example:
```java
Jwt jwt = jwtDecoder.decode(jwtStr);

String userId = jwt.getSubject();
String userEmail = jwt.getClaimAsString("email");
```

## JWT encoding with Nimbus
JWT encoder setup with secret:
```java
@Bean
public JwtEncoder jwtEncoder() {
    return new NimbusJwtEncoder(new ImmutableSecret<>(new SecretKeySpec(secret.getBytes(), "HmacSHA256")));
}

@Bean
public JwsHeader jwsHeader() {
    return JwsHeader.with(MacAlgorithm.HS256).build();
}
```
Encoding example:
```java
JwtClaimsSet claims = JwtClaimsSet.builder()
    .subject(user.getId())
    .claim("email", user.getEmail())
    .issuedAt(Instant.now())
    .expiresAt(Instant.now().plusSeconds(...))
    .build();

String jwt = jwtEncoder.encode(JwtEncoderParameters.from(jwsHeader, claims)).getTokenValue();
```
