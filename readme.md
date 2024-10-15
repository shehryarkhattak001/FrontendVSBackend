// const express = require("express");
// const jwt = require("jsonwebtoken");
// const mongoose = require("mongoose");
// const bodyParser = require("body-parser");
// const cors = require("cors");

// const jwtSecret = "123456"; // Change this to a secure key for production

// // Initialize Express App
// const app = express();
// const PORT = 3000;

// // Middleware to parse request bodies
// app.use(bodyParser.urlencoded({ extended: true }));
// app.use(express.json());

// // Enable CORS to allow cross-origin requests
// app.use(cors()); // Allow all origins by default

// // Serve static files (HTML, CSS, JS)
// app.use(express.static("."));

// // MongoDB Atlas connection
// mongoose
//   .connect(
//     "mongodb+srv://shery707:khan1122@cluster0.zcbkd.mongodb.net/userDB?retryWrites=true&w=majority"
//   )
//   .then(() => console.log("Connected to MongoDB Atlas successfully!"))
//   .catch((err) => console.error("Connection to MongoDB failed:", err));

// // Mongoose Schema and Model for User
// const userSchema = new mongoose.Schema({
//   firstName: { type: String, required: true },
//   lastName: { type: String, required: true },
//   email: { type: String, required: true, unique: true },
//   password: { type: String, required: true }, // Plain text passwords for now
// });

// const User = mongoose.model("User", userSchema);

// // Mongoose Schema and Model for Interest Calculation
// const interestSchema = new mongoose.Schema({
//   principal: { type: Number, required: true },
//   rate: { type: Number, required: true },
//   time: { type: Number, required: true },
//   createdAt: { type: Date, default: Date.now },
// });

// const Interest = mongoose.model("Interest", interestSchema);

// // Signup route
// app.post("/signup", async (req, res) => {
//   const { firstName, lastName, email, password } = req.body;

//   try {
//     if (!firstName || !lastName || !email || !password) {
//       return res.status(400).json({ message: "All fields are required." });
//     }

//     const existingUser = await User.findOne({ email });
//     if (existingUser) {
//       return res.status(400).json({ message: "Email already exists." });
//     }

//     const newUser = new User({
//       firstName,
//       lastName,
//       email,
//       password,
//     });

//     await newUser.save();
//     res.status(201).json({ message: "User created successfully!" });
//   } catch (error) {
//     res.status(500).json({ message: "Error signing up: " + error.message });
//   }
// });

// // Signin route with JWT
// // app.post("/signin", async (req, res) => {
// //   const { email, password } = req.body;

// //   try {
// //     const user = await User.findOne({ email });
// //     if (!user || password !== user.password) {
// //       return res.status(403).json({ message: "Invalid email or password." });
// //     }

// //     const token = jwt.sign({ email: user.email }, jwtSecret, {
// //       expiresIn: "1h",
// //     });
// //     res.json({ token });
// //   } catch (error) {
// //     res.status(500).json({ message: "Server error during signin." });
// //   }
// // });

// // Signin route with JWT
// app.post("/signin", async (req, res) => {
//   const { email, password } = req.body;

//   try {
//     const user = await User.findOne({ email });
//     if (!user || password !== user.password) {
//       return res.status(403).json({ message: "Invalid email or password." });
//     }

//     const token = jwt.sign({ email: user.email }, jwtSecret, {
//       expiresIn: "1h",
//     });
//     res.json({ token });
//   } catch (error) {
//     res.status(500).json({ message: "Server error during signin." });
//   }
// });

// // Interest rate calculation and data saving
// app.post("/interest", async (req, res) => {
//   const { principal, rate, time } = req.body;

//   if (!principal || !rate || !time) {
//     return res.status(400).json({ message: "All fields are required." });
//   }

//   const interest = (principal * rate * time) / 100;
//   const total = principal + interest;

//   // Save the interest calculation to MongoDB
//   const newInterest = new Interest({
//     principal,
//     rate,
//     time,
//   });

//   await newInterest.save();

//   res.status(201).json({
//     message: "Interest calculated successfully",
//     total: total,
//     interest: interest,
//   });
// });

// // Get all saved interest rates
// app.get("/interest-rates", async (req, res) => {
//   try {
//     const interestData = await Interest.find().sort({ createdAt: -1 });
//     res.json({ interestData });
//   } catch (error) {
//     res.status(500).json({ message: "Error fetching interest data." });
//   }
// });

// // Start the server
// app.listen(PORT, () => {
//   console.log(`Server is running on http://localhost:${PORT}`);
// });

// const express = require("express");
// const jwt = require("jsonwebtoken");
// const mongoose = require("mongoose");
// const bodyParser = require("body-parser");
// const cors = require("cors");

// const jwtSecret = "123456"; // Change this to a secure key for production

// // Initialize Express App
// const app = express();
// const PORT = 3000;

// // Middleware to parse request bodies
// app.use(bodyParser.urlencoded({ extended: true }));
// app.use(express.json());

// // Enable CORS to allow cross-origin requests
// app.use(cors()); // Allow all origins by default

// // Serve static files (HTML, CSS, JS)
// app.use(express.static("."));

// // MongoDB Atlas connection
// mongoose
//   .connect(
//     "mongodb+srv://shery707:khan1122@cluster0.zcbkd.mongodb.net/userDB?retryWrites=true&w=majority"
//   )
//   .then(() => console.log("Connected to MongoDB Atlas successfully!"))
//   .catch((err) => console.error("Connection to MongoDB failed:", err));

// // Mongoose Schema and Model for User
// const userSchema = new mongoose.Schema({
//   firstName: { type: String, required: true },
//   lastName: { type: String, required: true },
//   email: { type: String, required: true, unique: true },
//   password: { type: String, required: true }, // Plain text passwords
// });

// const User = mongoose.model("User", userSchema);

// // Mongoose Schema and Model for Interest Calculation
// const interestSchema = new mongoose.Schema({
//   principal: { type: Number, required: true },
//   rate: { type: Number, required: true },
//   time: { type: Number, required: true },
//   createdAt: { type: Date, default: Date.now },
// });

// const Interest = mongoose.model("Interest", interestSchema);

// // Signup route
// app.post("/signup", async (req, res) => {
//   const { firstName, lastName, email, password } = req.body;

//   try {
//     if (!firstName || !lastName || !email || !password) {
//       return res.status(400).json({ message: "All fields are required." });
//     }

//     const existingUser = await User.findOne({ email });
//     if (existingUser) {
//       return res.status(400).json({ message: "Email already exists." });
//     }

//     const newUser = new User({
//       firstName,
//       lastName,
//       email,
//       password, // Save password as plain text
//     });

//     await newUser.save();
//     res.status(201).json({ message: "User created successfully!" });
//   } catch (error) {
//     res.status(500).json({ message: "Error signing up: " + error.message });
//   }
// });

// // Signin route with plain text password comparison
// app.post("/signin", async (req, res) => {
//   const { email, password } = req.body;

//   try {
//     const user = await User.findOne({ email });
//     if (!user || password !== user.password) {
//       return res.status(403).json({ message: "Invalid email or password." });
//     }

//     const token = jwt.sign({ email: user.email }, jwtSecret, {
//       expiresIn: "1h",
//     });
//     res.json({ token });
//   } catch (error) {
//     res.status(500).json({ message: "Server error during signin." });
//   }
// });

// // Interest rate calculation and data saving
// app.post("/interest", async (req, res) => {
//   const { principal, rate, time } = req.body;

//   if (!principal || !rate || !time) {
//     return res.status(400).json({ message: "All fields are required." });
//   }

//   const interest = (principal * rate * time) / 100;
//   const total = principal + interest;

//   // Save the interest calculation to MongoDB
//   const newInterest = new Interest({
//     principal,
//     rate,
//     time,
//   });

//   await newInterest.save();

//   res.status(201).json({
//     message: "Interest calculated successfully",
//     total: total,
//     interest: interest,
//   });
// });

// // Get all saved interest rates
// app.get("/interest-rate", async (req, res) => {
//   try {
//     const interestData = await Interest.find().sort({ createdAt: -1 });
//     res.json({ interestData });
//   } catch (error) {
//     res.status(500).json({ message: "Error fetching interest data." });
//   }
// });

// // Start the server
// app.listen(PORT, () => {
//   console.log(`Server is running on http://localhost:${PORT}`);
// });
