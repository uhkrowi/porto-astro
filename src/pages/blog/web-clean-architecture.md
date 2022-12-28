---
layout: "../../layouts/BlogPost.astro"
title: "Clean Architecture"
pubDate: "Dec 12, 2022"
---

Clean Architecture is a software design philosophy that aims to separate the concerns of an application into distinct layers, with the goal of making the application more maintainable, testable, and scalable.

The basic structure of a clean architecture application is as follows:

The innermost layer is the domain layer, which contains the business logic and entities of the application. This layer should not depend on any other layers.

The next layer is the interface adapters layer, which contains the code that communicates with external systems, such as databases, APIs, and user interfaces. This layer should depend only on the domain layer.

The outermost layer is the frameworks and drivers layer, which contains the code that interfaces with the operating system and other external dependencies. This layer should depend only on the interface adapters layer.

By following this structure, the application can be more easily maintained and tested, as changes to the outer layers will not affect the inner layers.

Here is an example of a clean architecture application in Go:

- #### Domain Layer
The domain layer contains the business logic and entities of the application. It should not depend on any other layers.
```go
type User struct {
	ID   int
	Name string
}
```

- #### Interface Adapters Layer
The interface adapters layer contains the code that communicates with external systems, such as databases, APIs, and user interfaces. It should depend only on the domain layer.
```go
type UserRepository interface {
	Get(id int) (*User, error)
	Save(*User) error
}
```

- #### Frameworks and Drivers Layer

The frameworks and drivers layer contains the code that interfaces with the operating system and other external dependencies. It should depend only on the interface adapters layer.
```go
type HTTPHandler struct {
	repo UserRepository
}

func (h *HTTPHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	user, err := h.repo.Get(1)
	if err != nil {
		http.Error(w, err.Error(), http.StatusInternalServerError)
		return
	}

	w.Write([]byte(fmt.Sprintf("Hello, %s!", user.Name)))
}
```

#### Full code:
```go
type User struct {
	ID   int
	Name string
}

type UserRepository interface {
	Get(id int) (*User, error)
	Save(*User) error
}

type HTTPHandler struct {
	repo UserRepository
}

func (h *HTTPHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	user, err := h.repo.Get(1)
	if err != nil {
		http.Error(w, err.Error(), http.StatusInternalServerError)
		return
	}

	w.Write([]byte(fmt.Sprintf("Hello, %s!", user.Name)))
}
```

In this example, the `User` struct is part of the domain layer, the `UserRepository` interface is part of the interface adapters layer, and the `HTTPHandler` struct is part of the frameworks and drivers layer and depends on the `UserRepository` interface, which is part of the interface adapters layer, but not on the implementation of the repository, which allows the application to be more flexible and maintainable.

