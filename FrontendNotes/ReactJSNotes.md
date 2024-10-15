# React Components and Concepts: Comprehensive Notes with Real-World Examples

## 1. JSX, Components, Props, and State Management

### JSX (JavaScript XML)

**Real-world example:** Building a complex dashboard layout

```jsx
function DashboardLayout({ user, metrics, notifications }) {
  return (
    <div className="dashboard-container">
      <header>
        <h1>Welcome, {user.name}</h1>
        <NotificationBell count={notifications.length} />
      </header>
      <main>
        <MetricsOverview data={metrics} />
        <section className="dashboard-widgets">
          {metrics.map(metric => (
            <Widget key={metric.id} {...metric} />
          ))}
        </section>
      </main>
      <footer>
        <p>Last updated: {new Date().toLocaleString()}</p>
      </footer>
    </div>
  );
}
```

This example demonstrates how JSX allows you to create complex layouts with nested components and dynamic data rendering.

### Components

**Real-world example:** Reusable form input component with validation

```jsx
import React, { useState } from 'react';

function FormInput({ label, type, value, onChange, validate }) {
  const [error, setError] = useState('');

  const handleChange = (e) => {
    const newValue = e.target.value;
    onChange(newValue);
    const validationError = validate(newValue);
    setError(validationError);
  };

  return (
    <div className="form-group">
      <label>{label}</label>
      <input type={type} value={value} onChange={handleChange} className={error ? 'invalid' : ''} />
      {error && <span className="error-message">{error}</span>}
    </div>
  );
}

// Usage
function RegistrationForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const validateEmail = (email) => {
    return !email.includes('@') ? 'Invalid email address' : '';
  };

  const validatePassword = (password) => {
    return password.length < 8 ? 'Password must be at least 8 characters' : '';
  };

  return (
    <form>
      <FormInput
        label="Email"
        type="email"
        value={email}
        onChange={setEmail}
        validate={validateEmail}
      />
      <FormInput
        label="Password"
        type="password"
        value={password}
        onChange={setPassword}
        validate={validatePassword}
      />
      <button type="submit">Register</button>
    </form>
  );
}
```

This example shows how to create a reusable form input component that can be used across different forms with built-in validation.

### Props

**Real-world example:** Configurable data table component

```jsx
function DataTable({ columns, data, sortable, filterable, pagination }) {
  // Implementation details omitted for brevity

  return (
    <div className="data-table">
      {filterable && <FilterComponent onFilter={handleFilter} />}
      <table>
        <thead>
          <tr>
            {columns.map(column => (
              <th key={column.key}>
                {column.label}
                {sortable && <SortIndicator column={column.key} onSort={handleSort} />}
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {displayedData.map(row => (
            <tr key={row.id}>
              {columns.map(column => (
                <td key={`${row.id}-${column.key}`}>{row[column.key]}</td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
      {pagination && <PaginationControls {...paginationProps} />}
    </div>
  );
}

// Usage
function UserManagement() {
  const columns = [
    { key: 'name', label: 'Name' },
    { key: 'email', label: 'Email' },
    { key: 'role', label: 'Role' },
  ];

  const userData = [
    { id: 1, name: 'John Doe', email: 'john@example.com', role: 'Admin' },
    // ... more user data
  ];

  return (
    <DataTable
      columns={columns}
      data={userData}
      sortable={true}
      filterable={true}
      pagination={{ itemsPerPage: 10 }}
    />
  );
}
```

This example demonstrates how props can be used to create a highly configurable component that can be reused across different parts of an application with varying requirements.

### State Management

**Real-world example:** Complex form state management with nested fields

```jsx
import React, { useState } from 'react';

function ComplexForm() {
  const [formData, setFormData] = useState({
    personalInfo: {
      name: '',
      email: '',
      phone: '',
    },
    address: {
      street: '',
      city: '',
      country: '',
      postalCode: '',
    },
    preferences: {
      newsletter: false,
      theme: 'light',
    },
  });

  const handleChange = (section, field, value) => {
    setFormData(prevData => ({
      ...prevData,
      [section]: {
        ...prevData[section],
        [field]: value,
      },
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // Submit form data to API
    console.log('Submitting:', formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <section>
        <h2>Personal Information</h2>
        <input
          type="text"
          value={formData.personalInfo.name}
          onChange={(e) => handleChange('personalInfo', 'name', e.target.value)}
          placeholder="Name"
        />
        {/* More personal info fields */}
      </section>

      <section>
        <h2>Address</h2>
        <input
          type="text"
          value={formData.address.street}
          onChange={(e) => handleChange('address', 'street', e.target.value)}
          placeholder="Street"
        />
        {/* More address fields */}
      </section>

      <section>
        <h2>Preferences</h2>
        <label>
          <input
            type="checkbox"
            checked={formData.preferences.newsletter}
            onChange={(e) => handleChange('preferences', 'newsletter', e.target.checked)}
          />
          Subscribe to newsletter
        </label>
        <select
          value={formData.preferences.theme}
          onChange={(e) => handleChange('preferences', 'theme', e.target.value)}
        >
          <option value="light">Light</option>
          <option value="dark">Dark</option>
        </select>
      </section>

      <button type="submit">Submit</button>
    </form>
  );
}
```

This example shows how to manage complex, nested state in a form with multiple sections and different types of inputs.

## 2. Hooks: useState, useEffect, useContext, and Custom Hooks

### useState

**Real-world example:** Shopping cart state management

```jsx
function ShoppingCart() {
  const [cart, setCart] = useState([]);

  const addToCart = (product) => {
    setCart(prevCart => {
      const existingItem = prevCart.find(item => item.id === product.id);
      if (existingItem) {
        return prevCart.map(item =>
          item.id === product.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      } else {
        return [...prevCart, { ...product, quantity: 1 }];
      }
    });
  };

  const removeFromCart = (productId) => {
    setCart(prevCart => prevCart.filter(item => item.id !== productId));
  };

  const updateQuantity = (productId, newQuantity) => {
    setCart(prevCart =>
      prevCart.map(item =>
        item.id === productId
          ? { ...item, quantity: newQuantity }
          : item
      )
    );
  };

  // ... render cart items and total
}
```

This example demonstrates how useState can be used to manage a complex shopping cart state with add, remove, and update functionality.

### useEffect

**Real-world example:** Real-time data synchronization with WebSocket

```jsx
import React, { useState, useEffect } from 'react';
import io from 'socket.io-client';

function RealTimeTrading() {
  const [stockData, setStockData] = useState({});
  const [socket, setSocket] = useState(null);

  useEffect(() => {
    // Connect to WebSocket
    const newSocket = io('https://api.example.com/stocks');
    setSocket(newSocket);

    // Clean up on unmount
    return () => newSocket.close();
  }, []);

  useEffect(() => {
    if (!socket) return;

    // Listen for stock updates
    socket.on('stockUpdate', (data) => {
      setStockData(prevData => ({
        ...prevData,
        [data.symbol]: data,
      }));
    });

    // Request initial stock data
    socket.emit('subscribeStocks', ['AAPL', 'GOOGL', 'MSFT']);

    // Clean up listeners on unmount
    return () => {
      socket.off('stockUpdate');
    };
  }, [socket]);

  // ... render real-time stock data
}
```

This example shows how useEffect can be used to set up and manage WebSocket connections for real-time data updates.

### useContext

**Real-world example:** Global theme and language management

```jsx
import React, { createContext, useContext, useState } from 'react';

const AppContext = createContext();

export function AppProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const [language, setLanguage] = useState('en');

  const toggleTheme = () => {
    setTheme(prevTheme => prevTheme === 'light' ? 'dark' : 'light');
  };

  const changeLanguage = (lang) => {
    setLanguage(lang);
  };

  return (
    <AppContext.Provider value={{ theme, language, toggleTheme, changeLanguage }}>
      {children}
    </AppContext.Provider>
  );
}

export function useAppContext() {
  return useContext(AppContext);
}

// Usage in components
function Header() {
  const { theme, language, toggleTheme, changeLanguage } = useAppContext();

  return (
    <header className={`header-${theme}`}>
      <button onClick={toggleTheme}>Toggle Theme</button>
      <select value={language} onChange={(e) => changeLanguage(e.target.value)}>
        <option value="en">English</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
      </select>
    </header>
  );
}

function App() {
  return (
    <AppProvider>
      <Header />
      {/* Other components */}
    </AppProvider>
  );
}
```

This example demonstrates how useContext can be used to manage global application state like theme and language preferences.

### Custom Hooks

**Real-world example:** Custom hook for form validation

```jsx
import { useState, useEffect } from 'react';

function useFormValidation(initialState, validate) {
  const [values, setValues] = useState(initialState);
  const [errors, setErrors] = useState({});
  const [isSubmitting, setIsSubmitting] = useState(false);

  useEffect(() => {
    if (isSubmitting) {
      const noErrors = Object.keys(errors).length === 0;
      if (noErrors) {
        console.log('Form is valid! Submitting...', values);
        // You could call an API here
      } else {
        setIsSubmitting(false);
      }
    }
  }, [errors, isSubmitting, values]);

  function handleChange(event) {
    setValues({
      ...values,
      [event.target.name]: event.target.value
    });
  }

  function handleBlur() {
    const validationErrors = validate(values);
    setErrors(validationErrors);
  }

  function handleSubmit(event) {
    event.preventDefault();
    const validationErrors = validate(values);
    setErrors(validationErrors);
    setIsSubmitting(true);
  }

  return {
    handleSubmit,
    handleChange,
    handleBlur,
    values,
    errors,
    isSubmitting
  };
}

// Usage
function SignUpForm() {
  const { handleSubmit, handleChange, handleBlur, values, errors, isSubmitting } = useFormValidation(
    { email: '', password: '' },
    validateAuth
  );

  function validateAuth(values) {
    let errors = {};
    if (!values.email) {
      errors.email = 'Email is required';
    } else if (!/\S+@\S+\.\S+/.test(values.email)) {
      errors.email = 'Email address is invalid';
    }
    if (!values.password) {
      errors.password = 'Password is required';
    } else if (values.password.length < 6) {
      errors.password = 'Password must be at least 6 characters';
    }
    return errors;
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        onChange={handleChange}
        onBlur={handleBlur}
        value={values.email}
      />
      {errors.email && <p>{errors.email}</p>}
      <input
        name="password"
        type="password"
        onChange={handleChange}
        onBlur={handleBlur}
        value={values.password}
      />
      {errors.password && <p>{errors.password}</p>}
      <button type="submit" disabled={isSubmitting}>
        Sign Up
      </button>
    </form>
  );
}
```

This example shows how to create a custom hook for form validation that can be reused across different forms in an application.

## 3. Component Lifecycle: Understanding Mounting, Updating, and Unmounting Phases

In modern React with hooks, we don't explicitly define lifecycle methods, but we can still think about component lifecycle in terms of mounting, updating, and unmounting. Here's a real-world example that demonstrates all three phases:

**Real-world example:** Real-time chat application component

```jsx
import React, { useState, useEffect, useRef } from 'react';
import io from 'socket.io-client';

function ChatRoom({ roomId, userId }) {
  const [messages, setMessages] = useState([]);
  const [inputMessage, setInputMessage] = useState('');
  const socketRef = useRef();

  useEffect(() => {
    // Mounting phase
    console.log('ChatRoom mounted');
    
    // Connect to the chat room
    socketRef.current = io(`https://chat.example.com/room/${roomId}`);

    // Listen for incoming messages
    socketRef.current.on('message', (message) => {
      setMessages((msgs) => [...msgs, message]);
    });

    // Join the room
    socketRef.current.emit('joinRoom', { userId, roomId });

    // Cleanup function (Unmounting phase)
    return () => {
      console.log('ChatRoom unmounting');
      socketRef.current.emit('leaveRoom', { userId, roomId });
      socketRef.current.disconnect();
    };
  }, [roomId, userId]);

  useEffect(() => {
    // Updating phase
    console.log('Messages updated:', messages);
    
    // Scroll to bottom of message list
    const messageList = document.getElementById('message-list');
    messageList.scrollTop = messageList.scrollHeight;
  }, [messages]);

  const sendMessage = (e) => {
    e.preventDefault();
    if (inputMessage.trim()) {
      socketRef.current.emit('sendMessage', {
        roomId,
        userId,
        text: inputMessage
      });
      setInputMessage('');
    }
  };

  return (
    <div className="chat-room">
      <div id="message-list" className="message-list">
        {messages.map((msg, index) => (
          <div key={index} className={`message ${msg.userId === userId ? 'own-message' : ''}`}>
            <span className="user">{msg.userId}</span>
            <p>{msg.text}</p>
          </div>
        ))}
      </div>
      <form onSubmit={sendMessage}>
        <input
          type="text"
          value={inputMessage}
          onChange={(e) => setInputMessage(e.target.value)}
          placeholder="Type a message..."
        />
        <button type="submit">Send</button>
      </form>
    </div>
  );
}
```

This ChatRoom component demonstrates all three lifecycle phases:

1. **Mounting:** When the component mounts, it connects to the chat room using a WebSocket, sets up event listeners, and joins the room.
2. **Updating:** When new messages are received or sent, the component updates its state and scrolls the message list to the bottom.
3. **Unmounting:** When the component unmounts (e.g., user leaves the chat room), it performs cleanup by leaving the room and disconnecting the WebSocket.

## 4. Conditional Rendering: Handling if/else Logic, Ternary Operators in JSX

**Real-world example:** User authentication and role-based content rendering

```jsx
import React, { useState, useEffect } from 'react';
import { useAuth } from './auth-context'; // Assume we have an auth context

function Dashboard() {
  const { user, isLoading, error } = useAuth();
  const [userContent, setUserContent] = useState(null);

  useEffect(() => {
    if (user) {
      fetchUserContent(user.id).then(setUserContent);
    }
  }, [user]);

  if (isLoading) {
    return <LoadingSpinner />;
  }

  if (error) {
    return <ErrorMessage message={error.message} />;
  }

  return (
    <div className="dashboard">
      <header>
        <h1>Welcome to Your Dashboard</h1>
        {user ? (
          <UserMenu user={user} />
        ) : (
          <LoginButton />
        )}
      </header>

      <main>
        {user ? (
          <>
            <UserProfile user={user} />
            {user.role === 'admin' && <AdminPanel />}
            {user.role === 'manager' ? (
              <ManagerDashboard data={userContent} />
            ) : (
              <EmployeeDashboard data={userContent} />
            )}
          </>
        ) : (
          <LandingPage />
        )}
      </main>

      <footer>
        {user?.subscription === 'premium' && <PremiumSupport />}
      </footer>
    </div>
  );
}

function UserMenu({ user }) {
  return (
    <div className="user-menu">
      <img src={user.avatarUrl} alt={user.name} />
      <span>{user.name}</span>
      <LogoutButton />
    </div>
  );
}

function AdminPanel() {
  return <div className="admin-panel">Admin-specific content</div>;
}

function ManagerDashboard({ data }) {
  return <div className="manager-dashboard">Manager-specific content with {data}</div>;
}

function EmployeeDashboard({ data }) {
  return <div className="employee-dashboard">Employee-specific content with {data}</div>;
}

function LandingPage() {
  return <div className="landing-page">Welcome! Please log in to access your dashboard.</div>;
}

function PremiumSupport() {
  return <div className="premium-support">24/7 Premium Support Available</div>;
}
```

This example demonstrates various conditional rendering techniques:

1. If/else logic for loading and error states.
2. Ternary operators for user authentication status (logged in vs. not logged in).
3. Logical AND (`&&`) operator for rendering admin-specific content.
4. Nested ternary for manager vs. employee dashboard.
5. Optional chaining with logical AND for premium subscription features.

## 5. Controlled/Uncontrolled Components and Event Handling

**Real-world example:** Advanced form with both controlled and uncontrolled components

```jsx
import React, { useState, useRef } from 'react';

function AdvancedForm() {
  // Controlled components
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    preferences: {
      newsletter: false,
      notifications: 'email'
    }
  });

  // Uncontrolled components
  const fileInputRef = useRef(null);
  const termsRef = useRef(null);

  const handleInputChange = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData(prevData => ({
      ...prevData,
      [name]: type === 'checkbox' ? checked : value
    }));
  };

  const handlePreferenceChange = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData(prevData => ({
      ...prevData,
      preferences: {
        ...prevData.preferences,
        [name]: type === 'checkbox' ? checked : value
      }
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    
    // Access uncontrolled component values
    const file = fileInputRef.current.files[0];
    const agreedToTerms = termsRef.current.checked;

    // Combine controlled and uncontrolled data
    const submitData = {
      ...formData,
      file: file ? file.name : null,
      agreedToTerms
    };

    console.log('Submitting form data:', submitData);
    // Here you would typically send the data to an API
  };

  return (
    <form onSubmit={handleSubmit} className="advanced-form">
      <div className="form-group">
        <label htmlFor="name">Name:</label>
        <input
          type="text"
          id="name"
          name="name"
          value={formData.name}
          onChange={handleInputChange}
          required
        />
      </div>

      <div className="form-group">
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          name="email"
          value={formData.email}
          onChange={handleInputChange}
          required
        />
      </div>

      <div className="form-group">
        <label>
          <input
            type="checkbox"
            name="newsletter"
            checked={formData.preferences.newsletter}
            onChange={handlePreferenceChange}
          />
          Subscribe to newsletter
        </label>
      </div>

      <div className="form-group">
        <label>Notification Preference:</label>
        <select
          name="notifications"
          value={formData.preferences.notifications}
          onChange={handlePreferenceChange}
        >
          <option value="email">Email</option>
          <option value="sms">SMS</option>
          <option value="push">Push Notification</option>
        </select>
      </div>

      <div className="form-group">
        <label htmlFor="file">Upload File:</label>
        <input
          type="file"
          id="file"
          ref={fileInputRef}
        />
      </div>

      <div className="form-group">
        <label>
          <input
            type="checkbox"
            ref={termsRef}
            required
          />
          I agree to the terms and conditions
        </label>
      </div>

      <button type="submit">Submit</button>
    </form>
  );
}
```

This example demonstrates:

1. Controlled components (name, email, preferences) using useState.
2. Uncontrolled components (file input, terms checkbox) using useRef.
3. Complex state management for nested form data.
4. Event handling for various input types (text, checkbox, select, file).
5. Form submission combining both controlled and uncontrolled component data.

These real-world examples should provide a more comprehensive understanding of how these React concepts are applied in complex, production-like scenarios. They demonstrate how different React features can be combined to create sophisticated user interfaces and manage complex application state.


## 6. React Router, Route Parameters, and Nested Routing

**Real-world example:** E-commerce application routing

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Switch, Link, useParams, useRouteMatch } from 'react-router-dom';

// Main App component
function EcommerceApp() {
  return (
    <Router>
      <div className="ecommerce-app">
        <nav>
          <ul>
            <li><Link to="/">Home</Link></li>
            <li><Link to="/products">Products</Link></li>
            <li><Link to="/cart">Cart</Link></li>
            <li><Link to="/account">My Account</Link></li>
          </ul>
        </nav>

        <Switch>
          <Route exact path="/" component={Home} />
          <Route path="/products" component={ProductsSection} />
          <Route path="/cart" component={Cart} />
          <Route path="/account" component={Account} />
          <Route component={NotFound} />
        </Switch>
      </div>
    </Router>
  );
}

// Products section with nested routes
function ProductsSection() {
  let { path, url } = useRouteMatch();

  return (
    <div className="products-section">
      <h2>Products</h2>
      <ul>
        <li><Link to={`${url}/category/electronics`}>Electronics</Link></li>
        <li><Link to={`${url}/category/clothing`}>Clothing</Link></li>
        <li><Link to={`${url}/category/books`}>Books</Link></li>
      </ul>

      <Switch>
        <Route exact path={path}>
          <h3>Select a category</h3>
        </Route>
        <Route path={`${path}/category/:categoryId`}>
          <Category />
        </Route>
        <Route path={`${path}/product/:productId`}>
          <ProductDetails />
        </Route>
      </Switch>
    </div>
  );
}

// Category component using route parameters
function Category() {
  let { categoryId } = useParams();

  return (
    <div className="category">
      <h3>{categoryId} Products</h3>
      {/* Fetch and display products for this category */}
    </div>
  );
}

// ProductDetails component using route parameters
function ProductDetails() {
  let { productId } = useParams();

  return (
    <div className="product-details">
      <h3>Product Details for ID: {productId}</h3>
      {/* Fetch and display product details */}
    </div>
  );
}

// Account section with nested routes
function Account() {
  let { path, url } = useRouteMatch();

  return (
    <div className="account-section">
      <h2>My Account</h2>
      <ul>
        <li><Link to={`${url}/profile`}>Profile</Link></li>
        <li><Link to={`${url}/orders`}>Orders</Link></li>
        <li><Link to={`${url}/settings`}>Settings</Link></li>
      </ul>

      <Switch>
        <Route exact path={path}>
          <h3>Select an account section</h3>
        </Route>
        <Route path={`${path}/profile`} component={Profile} />
        <Route path={`${path}/orders`} component={Orders} />
        <Route path={`${path}/settings`} component={Settings} />
      </Switch>
    </div>
  );
}

// Other components (Home, Cart, Profile, Orders, Settings, NotFound) would be defined here
```

This example demonstrates:

1. Setting up main routes for an e-commerce application.
2. Using nested routes for product categories and account sections.
3. Utilizing route parameters for dynamic content (`:categoryId` and `:productId`).
4. Using `useRouteMatch` for nested routing.
5. Using `useParams` to access route parameters.

## 7. Context API, Lifting State Up, Redux (if applicable)

**Real-world example:** Global state management for an e-commerce application

First, let's implement this using Context API:

```jsx
import React, { createContext, useContext, useReducer } from 'react';

// Create contexts
const CartContext = createContext();
const UserContext = createContext();

// Reducers
function cartReducer(state, action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return [...state, action.payload];
    case 'REMOVE_FROM_CART':
      return state.filter(item => item.id !== action.payload.id);
    case 'CLEAR_CART':
      return [];
    default:
      return state;
  }
}

function userReducer(state, action) {
  switch (action.type) {
    case 'LOGIN':
      return action.payload;
    case 'LOGOUT':
      return null;
    case 'UPDATE_PROFILE':
      return { ...state, ...action.payload };
    default:
      return state;
  }
}

// Provider component
function AppProvider({ children }) {
  const [cart, cartDispatch] = useReducer(cartReducer, []);
  const [user, userDispatch] = useReducer(userReducer, null);

  return (
    <UserContext.Provider value={{ user, userDispatch }}>
      <CartContext.Provider value={{ cart, cartDispatch }}>
        {children}
      </CartContext.Provider>
    </UserContext.Provider>
  );
}

// Custom hooks to use the contexts
function useCart() {
  const context = useContext(CartContext);
  if (!context) {
    throw new Error('useCart must be used within a CartProvider');
  }
  return context;
}

function useUser() {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('useUser must be used within a UserProvider');
  }
  return context;
}

// Example usage in components
function ProductList() {
  const { cartDispatch } = useCart();

  const addToCart = (product) => {
    cartDispatch({ type: 'ADD_TO_CART', payload: product });
  };

  // Render product list and use addToCart function
}

function Cart() {
  const { cart, cartDispatch } = useCart();

  const removeFromCart = (product) => {
    cartDispatch({ type: 'REMOVE_FROM_CART', payload: product });
  };

  // Render cart items and use removeFromCart function
}

function UserProfile() {
  const { user, userDispatch } = useUser();

  const updateProfile = (updates) => {
    userDispatch({ type: 'UPDATE_PROFILE', payload: updates });
  };

  // Render user profile and use updateProfile function
}

// Main App component
function App() {
  return (
    <AppProvider>
      <Header />
      <ProductList />
      <Cart />
      <UserProfile />
    </AppProvider>
  );
}
```

This example demonstrates:

1. Using Context API for global state management.
2. Creating separate contexts for different concerns (cart and user).
3. Using reducers with context for more complex state management.
4. Creating custom hooks for easy context consumption.

Now, let's see how this could be implemented using Redux:

```jsx
import { createStore, combineReducers } from 'redux';
import { Provider, useSelector, useDispatch } from 'react-redux';

// Action creators
const addToCart = (product) => ({ type: 'ADD_TO_CART', payload: product });
const removeFromCart = (productId) => ({ type: 'REMOVE_FROM_CART', payload: productId });
const login = (userData) => ({ type: 'LOGIN', payload: userData });
const logout = () => ({ type: 'LOGOUT' });
const updateProfile = (updates) => ({ type: 'UPDATE_PROFILE', payload: updates });

// Reducers
function cartReducer(state = [], action) {
  switch (action.type) {
    case 'ADD_TO_CART':
      return [...state, action.payload];
    case 'REMOVE_FROM_CART':
      return state.filter(item => item.id !== action.payload);
    default:
      return state;
  }
}

function userReducer(state = null, action) {
  switch (action.type) {
    case 'LOGIN':
      return action.payload;
    case 'LOGOUT':
      return null;
    case 'UPDATE_PROFILE':
      return { ...state, ...action.payload };
    default:
      return state;
  }
}

const rootReducer = combineReducers({
  cart: cartReducer,
  user: userReducer,
});

const store = createStore(rootReducer);

// Example usage in components
function ProductList() {
  const dispatch = useDispatch();

  const handleAddToCart = (product) => {
    dispatch(addToCart(product));
  };

  // Render product list and use handleAddToCart function
}

function Cart() {
  const cart = useSelector(state => state.cart);
  const dispatch = useDispatch();

  const handleRemoveFromCart = (productId) => {
    dispatch(removeFromCart(productId));
  };

  // Render cart items and use handleRemoveFromCart function
}

function UserProfile() {
  const user = useSelector(state => state.user);
  const dispatch = useDispatch();

  const handleUpdateProfile = (updates) => {
    dispatch(updateProfile(updates));
  };

  // Render user profile and use handleUpdateProfile function
}

// Main App component
function App() {
  return (
    <Provider store={store}>
      <Header />
      <ProductList />
      <Cart />
      <UserProfile />
    </Provider>
  );
}
```

This Redux example demonstrates:

1. Creating a Redux store with combined reducers.
2. Defining action creators for various actions.
3. Using `useSelector` to access state and `useDispatch` to dispatch actions.
4. Wrapping the app with a Redux `Provider`.

Both the Context API and Redux examples show how to manage global state in a complex application, allowing data to be easily shared and updated across components.

## 8. Memoization (React.memo, useMemo, useCallback)

**Real-world example:** Optimizing a dashboard with complex calculations

```jsx
import React, { useState, useMemo, useCallback } from 'react';

// Expensive calculation function
const calculateAnalytics = (data) => {
  console.log('Calculating analytics...');
  // Simulate expensive calculation
  let result = 0;
  for (let i = 0; i < 1000000; i++) {
    result += data.reduce((sum, item) => sum + item.value, 0);
  }
  return result;
};

// Memoized child component
const AnalyticsChart = React.memo(function AnalyticsChart({ data, onItemClick }) {
  console.log('Rendering AnalyticsChart');
  return (
    <div className="analytics-chart">
      <h3>Analytics Chart</h3>
      <ul>
        {data.map(item => (
          <li key={item.id} onClick={() => onItemClick(item.id)}>
            {item.name}: {item.value}
          </li>
        ))}
      </ul>
    </div>
  );
});

function Dashboard() {
  const [data, setData] = useState([
    { id: 1, name: 'Product A', value: 100 },
    { id: 2, name: 'Product B', value: 200 },
    { id: 3, name: 'Product C', value: 300 },
  ]);
  const [selectedId, setSelectedId] = useState(null);

  // Memoized expensive calculation
  const analyticsResult = useMemo(() => calculateAnalytics(data), [data]);

  // Memoized callback for child component
  const handleItemClick = useCallback((id) => {
    setSelectedId(id);
    console.log(`Item ${id} clicked`);
  }, []);

  return (
    <div className="dashboard">
      <h2>Sales Dashboard</h2>
      <p>Total Analytics Value: {analyticsResult}</p>
      <AnalyticsChart data={data} onItemClick={handleItemClick} />
      {selectedId && <p>Selected Item: {selectedId}</p>}
      <button onClick={() => setData([...data, { id: Date.now(), name: 'New Product', value: Math.random() * 100 }])}>
        Add Random Product
      </button>
    </div>
  );
}
```

This example demonstrates:

1. Using `useMemo` to memoize the result of an expensive calculation (`calculateAnalytics`). The calculation will only re-run when the `data` changes.
2. Using `React.memo` to memoize the `AnalyticsChart` component. It will only re-render if its props change.
3. Using `useCallback` to memoize the `handleItemClick` function. This ensures that the function reference remains stable across re-renders, preventing unnecessary re-renders of the `AnalyticsChart` component.

These optimizations are particularly useful in scenarios where:

- You have expensive calculations that don't need to be re-run on every render.
- You have child components that receive function props, which would normally cause them to re-render unnecessarily.
- You want to optimize the rendering of complex list items or charts that don't change frequently.

By applying these memoization techniques, you can significantly improve the performance of your React applications, especially when dealing with large datasets or complex UI interactions.

