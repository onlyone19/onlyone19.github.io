---
title: quarkus - Restful API and CDI
---

# Step 2: Restful API and CDI
Quarkus is not a full CDI implementation. Only a subset of features is implemented. 

## bean defining annotations
Bean classes that don’t have a bean defining annotation are not discovered. 
- @ApplicationScoped, @SessionScoped, @ConversationScoped and @RequestScoped annotations,
- all other normal scope types,
- @Interceptor and @Decorator annotations,
- all stereotype annotations (i.e. annotations annotated with @Stereotype),
- and the @Dependent scope annotation.

## list of supported features
- Programming model
  + Managed beans implemented by a Java class
     * @PostConstruct and @PreDestroy lifecycle callbacks
  + Producer methods and fields, disposers
  + Qualifiers
  + Alternatives
  + Stereotypes
- Dependency injection and lookup
  + Field, constructor and initializer/setter injection
  + Type-safe resolution
  + Programmatic lookup via javax.enterprise.inject.Instance
  + Client proxies
  + Injection point metadata
- Scopes and contexts
  + @Dependent, @ApplicationScoped, @Singleton, @RequestScoped and @SessionScoped
  + Custom scopes and contexts
- Interceptors
  + Business method interceptors: @AroundInvoke
  + Interceptors for lifecycle event callbacks: @PostConstruct, @PreDestroy, @AroundConstruct
- Events and observer methods, including asynchronous events and transactional observer methods

## list of limitations
- @ConversationScoped is not supported
- Decorators are not supported
- Portable Extensions are not supported
- BeanManager - only the following methods are implemented: getBeans(), createCreationalContext(), getReference(), getInjectableReference() , resolve(), getContext(), fireEvent(), getEvent() and createInstance()
- Specialization is not supported
- beans.xml descriptor content is ignored
- Passivation and passivating scopes are not supported
- Interceptor methods on superclasses are not implemented yet


