- We will make an account for you. You'll receive a username & password.
- You can use that account to log into the club, and use the GraphQL browser: `/graphql/browser/club`.
- The browser contains the Docs, because GraphQL is technically self-documenting.
- The GraphQL endpoint is `/graphql/club`.
- Authentication is simple HTTP Basic auth with your username & password.
- Every API request **must** include the `User-agent` header.
- See https://graphql.org/learn/serving-over-http/#post-request-and-body for the structure of every request.
- Warnings & deprecations are in `extensions.warnings`. Try `query { me { deprecated_test } }`
- API limits: 500 requests per day (that's 1 per 3 minutes). You can fetch intelligently, and cache the results.
- Follow this repo for announcements/changes/deprecations. We will create a Release for every announcement, so 'Watch' the repo for that.

**Play around with the browser!** It's brilliant. When that works, including using _variables_, use the real API.

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

Use `createReservation`. See inline docs in the browser. **NOTE** You should use GraphQL's _variables_, not inline data.
