- We will make an account for you. You'll receive a username & password.
- You can use that account to log into the club, and use the GraphQL browser: `/graphql/browser/club`.
- The browser contains the Docs, because GraphQL is technically self-documenting.
- The GraphQL endpoint is `/graphql/club`.
- Authentication is simple HTTP Basic auth with your username & password.
- See https://graphql.org/learn/serving-over-http/#post-request for the structure of every request.

## Availability

You can fetch availability in 2 ways:

- `availability`- Get a technical summary of a date's schedule. Example:

```
query {
  availability(dates: ["2020-08-31"], resources: [2853]) {
    dates {
      date
      resources {
        resource {
          name
        }
        slots(group: TYPE) {
          start_time
          end_time
          status
        }
      }
    }
  }
}
```

- `court_reservations` - Get all reservations, new since X, or all on a date. Example:

```
query {
  court_reservations(dates: ["2020-08-31"], resources: [2853]) {
    total
    nodes {
      resource {
        name
      }
      start_time
      end_time
    }
  }
}
```

## Create reservations

Use `createReservation`. See inline docs in the browser. **NOTE** You should use GraphQL's `arguments`, not inline data.
