// Import dependencies
import React, { useState, useEffect } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import { PayPalButton } from "react-paypal-button-v2";

// Home Page - Welcome page
function Home() {
  return (
    <div>
      <h1>Welcome to Electrician Connect</h1>
      <p>Where verified electricians and clients connect for quality services.</p>
      <button onClick={() => window.location.href='/signup'}>Get Started</button>
    </div>
  );
}

// Sign Up Page - Sign up form for both clients and electricians
function SignUp() {
  return (
    <div>
      <h2>Sign Up</h2>
      <form>
        <label htmlFor="role">I am a:</label>
        <select id="role" name="role">
          <option value="client">Client</option>
          <option value="electrician">Electrician</option>
        </select>
        <label htmlFor="name">Name:</label>
        <input type="text" id="name" name="name" />
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" name="email" />
        <label htmlFor="location">Location:</label>
        <input type="text" id="location" name="location" />
        <label htmlFor="password">Password:</label>
        <input type="password" id="password" name="password" />
        <button type="submit">Sign Up</button>
      </form>
    </div>
  );
}

// Login Page - Allow user to log in
function Login() {
  return (
    <div>
      <h2>Login</h2>
      <form>
        <label htmlFor="email">Email:</label>
        <input type="email" id="email" name="email" />
        <label htmlFor="password">Password:</label>
        <input type="password" id="password" name="password" />
        <button type="submit">Login</button>
      </form>
    </div>
  );
}

// Job Posting Page - Clients can post the scope of work
function PostJob() {
  return (
    <div>
      <h2>Post a Job</h2>
      <form>
        <label htmlFor="jobTitle">Job Title:</label>
        <input type="text" id="jobTitle" name="jobTitle" />
        <label htmlFor="description">Description:</label>
        <textarea id="description" name="description"></textarea>
        <label htmlFor="budget">Budget:</label>
        <input type="number" id="budget" name="budget" />
        <label htmlFor="location">Location:</label>
        <input type="text" id="location" name="location" />
        <button type="submit">Post Job</button>
      </form>
    </div>
  );
}

// Job Bidding Page - Electricians can bid on jobs
function JobBids() {
  const [bids, setBids] = useState([]);

  useEffect(() => {
    // Fetch available job bids from backend (dummy data for now)
    setBids([
      { id: 1, title: "Wiring Repair", budget: "$500" },
      { id: 2, title: "Panel Upgrade", budget: "$1200" }
    ]);
  }, []);

  return (
    <div>
      <h2>Available Jobs</h2>
      <ul>
        {bids.map(bid => (
          <li key={bid.id}>
            <h3>{bid.title}</h3>
            <p>Budget: {bid.budget}</p>
            <button>Bid Now</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

// Subscription Page - Clients and Electricians subscribe for access
function Subscription() {
  return (
    <div>
      <h2>Subscribe to Unlock Profiles and Job Listings</h2>
      <PayPalButton
        amount="10.00"
        onSuccess={(details, data) => {
          alert("Transaction completed by " + details.payer.name.given_name);
        }}
      />
    </div>
  );
}

// Rating and Review Page - Clients leave reviews for electricians
function ReviewPage() {
  const [reviews, setReviews] = useState([]);

  useEffect(() => {
    // Fetch reviews from backend (dummy data for now)
    setReviews([
      { id: 1, client: "John Doe", rating: 5, comment: "Excellent work!" },
      { id: 2, client: "Jane Smith", rating: 4, comment: "Good, but room for improvement." }
    ]);
  }, []);

  return (
    <div>
      <h2>Electrician Reviews</h2>
      <ul>
        {reviews.map(review => (
          <li key={review.id}>
            <h3>{review.client}</h3>
            <p>Rating: {review.rating}</p>
            <p>{review.comment}</p>
          </li>
        ))}
      </ul>
    </div>
  );
}

// Payment Page - Clients pay electricians through the app, commission auto-deducted
function Payment() {
  return (
    <div>
      <h2>Make a Payment</h2>
      <p>Payment for completed jobs</p>
      <PayPalButton
        amount="500.00"  // Example amount
        onSuccess={(details, data) => {
          alert("Payment successful. Commission auto-deducted.");
        }}
      />
    </div>
  );
}

// Admin Panel - Administrator can monitor activity and commissions
function AdminPanel() {
  const [subscriptions, setSubscriptions] = useState([]);
  const [payments, setPayments] = useState([]);

  useEffect(() => {
    // Fetch subscription and payment data from backend (dummy data for now)
    setSubscriptions([{ id: 1, user: "Client1", amount: "$10" }]);
    setPayments([{ id: 1, electrician: "Electrician1", amount: "$500", commission: "$50" }]);
  }, []);

  return (
    <div>
      <h2>Admin Dashboard</h2>
      <h3>Subscriptions</h3>
      <ul>
        {subscriptions.map(sub => (
          <li key={sub.id}>
            {sub.user} - {sub.amount}
          </li>
        ))}
      </ul>
      <h3>Payments</h3>
      <ul>
        {payments.map(pay => (
          <li key={pay.id}>
            {pay.electrician} - {pay.amount} (Commission: {pay.commission})
          </li>
        ))}
      </ul>
    </div>
  );
}

// Main App Component - Routing setup
function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/signup" component={SignUp} />
        <Route path="/login" component={Login} />
        <Route path="/post-job" component={PostJob} />
        <Route path="/job-bids" component={JobBids} />
        <Route path="/subscription" component={Subscription} />
        <Route path="/reviews" component={ReviewPage} />
        <Route path="/payment" component={Payment} />
        <Route path="/admin" component={AdminPanel} />
      </Switch>
    </Router>
  );
}

export default App;
