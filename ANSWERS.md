## 1.

The current implementation keeps all orders in an in-memory array, which is fine for a small demo but would not work well in a production system. If the application had thousands of orders and many users accessing it at the same time, I would move the data to a database such as PostgreSQL or MySQL. This would ensure that data is persisted and not lost when the server restarts.

Overall, these changes would make the system more reliable, scalable, and better suited for handling large amounts of data and concurrent users.

## 2.

Returning either an `Order` object or an `{ error: string }` object works for a simple application, but it makes the API response inconsistent. The frontend has to check the response type every time, which can become difficult to manage as the application grows. In a real-world API, I would use proper HTTP status codes and NestJS exceptions. For example, if an order is not found, the API should return a 404 status with a clear error message. This makes the API more predictable, easier to consume, and aligned with standard REST practices.

## 3. 

For a larger dashboard, I would avoid making API calls directly inside components. Instead, I would create a separate API/service layer to handle backend requests and use custom hooks for data fetching. I would break the UI into reusable components for filters, tables, and pagination. For shared state and caching, I would use a state management solution such as Context API or Redux. This structure keeps the code organized, easier to maintain, and simpler to extend as new features and API calls are added.

## 4.

The current `Order` and `Garment` models are very basic and do not cover many real-world laundry scenarios. Important fields such as customer contact information, payment status, order total, pickup/delivery dates, and special instructions are missing. For garments, fields like quantity, price, damage notes, and status history would be useful. The model should also handle cases such as partial order completion, lost garments, or re-cleaning requests. Adding these fields and relationships would make the system more realistic and better suited for actual laundry operations.

## 5. 

AI generated code can speed up development, but it may contain bugs, security issues, incorrect logic, or miss important edge cases. Developers might also rely on code they do not fully understand, making maintenance more difficult. Before deploying to production, I would carefully review the code, test different scenarios, verify that it meets business requirements. AI-generated code should be treated as a starting point and always validated by a developer.

## 6. 

The current REST API requires the frontend to repeatedly fetch data to see status changes. For near real-time updates, I would use WebSockets so the server can immediately notify connected clients when a garment's status changes. This would provide a better user experience and reduce unnecessary requests. Another simpler option is polling, where the frontend refreshes data every few seconds, but this generates extra network traffic. The choice depends on the application's scale and how important real-time updates are to the business.