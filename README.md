# Frontend-project
db.js
import mongoose from
“
mongoose";
const connectDB = async ()=>f
try f
await
mongoose.connect("mongodb://1ocalhost:2
7017/formValidationDB");
console.log("国 MongoDB Connected”)；
） catch (error)f
console.error("X MongoDB Connection
Failed:"
, error.message);
process.exit(1)；
i
export default connectDB;
import React from"react";
export default function SuccessMessage(f
message ))f
return(
<div className="bg-green-200 text-green
-800 p-2 rounded mb-4 text-center">
fmessage)
</div>
)；
useemodel.js
import React from"react";
import FormValidation from
"./components/FormValidation";
function App()[
return <FormValidation />;
export default App;
module.exports =f
content:["./src/**/*.(js, jsx, ts, tsx"],
theme:f extend:0)，
plugins:[],
};
usercontroller.js
import User from "../models/userModel.js";
1/ Register User
export const registerUser = async (req, res)
=>(
const f name, email, password,
confirmPassword )= req.body;
1/ Server-side validation
if (!name ll !email Il Ipassword ll
!confirmPassword)f
return res.status(400).json(f message: "All
fields are required"1);
if (password !== confirmPassword)f
return res.status(400). json([ message:
"Passwords do not match"1);
tryf
const userExists = await User.findOne(f
email);
if (userExists)
return res.status(400).json(f message:
"Email already registered"1);
const user = await User.create(f name, email,
password 3);
res.status(201).json(f message:"Registration
Successful"
, user ));
) catch (error)(
res.status(500). json(( message: "Server
error"
, error: error.message ));
}
}
ErrorMiddleware.js
import express from "express";
import f registeruser )
from"../controllers/userController.js";const
router = express.Router()；
router.post("/register
”
,registerUser);export
default router;
export const notFound = (req, res, next)=>[
const error = new Error(Not Found - $freq.originalUr1));res.status(404)；
next(error);
export const errorHandler = (err, req, res,
next) =>f
const statusCode = res.statusCode === 200 ?
500:res.statusCode;
res.status(statusCode)；
res.json(f message: err.message, stack:
process.env.NODE_ENV
==="production"?null:err.stack 3);
Server.js
import express from"express";import cors
from
“
cors";
import connectDB from"./config/db.js";
import userRoutes
from"./routes/userRoutes.js";
import f notFound, errorHandler f from
"./middleware/errorMiddleware.js";
connectDB()；
const app = express()；
app.use(cors());；
app.use(express.json())；
app.use("/api/users"
, userRoutes);
app.use(notFound)；
app.use(errorHandler);
const PORT = process.env.PORT IL 5000;
app.listen(PORT, () =>console.log(①
Server running on port $fPORTY));
}
FormValidation.js
import React, f usestate ) from
“
react";Import axios from "axios";
import SuccessNessage from
“
,/SuccessMessage";
export default function FormValidation()1
const [formData, setFormData] = useState(f
name:""
, email:""
,password:""
,
confirmPassword:"" 1);
const [errors, setErrors] = useState(0)；
const [success, setSuccess] =
useState("")；I/ Validation rules
const validate = (name, value) =>f
switch (name) f
case "name":
return value.length< 3 ? "Name must be at
least 3 characters"："";case"email":
return /^[시 Se]+@[^1S@]+1.[시
s@]+9/.test(value)?"": “Invalid ema11";case
"password":
return value, length < 6 ? "Password must be
6+ characters" :"";case
“
confirmPassword":
return value lss formData, password ?
“Passwords do not match" ；
“";default;
return""；
const handleChange = (e) =>f
const f name, value )= e.target;
const error = validate(name, value)；
setErrors(t ...errors, [name]:error );
setFormData(f...formData, [name]:value );
const handlesubmit u async (e) ! 一
e.preventDefault()：
if (0bject. values(errors).some((err) =》 err
!=="")) return alert("Fix validation errors
first");
try f
const f data)= await
axios.post("http://1ocalhost:5000/api/users/r
egister
”
, formData);setSuccess(data,
message);
setFormData(( name：""
, email:""
,
password:""
,confirmPassword:""));
setErrors(0)；
） catch (err)t
setsuccess(err .response? . data? . message
"Error occurred")s
return(
(div className="max-w-md mx-auto mt-
10 p-6 border rounded-xl shadow-Ig bg- white"y
<h2 className="text-2x1 font-bold text- center mb-5">Interact ive Form
Validation</h2>
[success && <SuccessMessage message-
(success) />)
<form onSubmit=(handleSubmit)
className="space-y-4">
f["name
”
,
“
email"
,
“
password"
,
“
confirmPassword"].map((field) =>(
<diy kev=ffield>
<input
type=(field. includes("password") ?
"password" :"text")
name=(fieldl
placeholder=(field.replace(/([A-Z])/g,
" $1"))
value=fformData[field])
onChange=(handleChange)
className=[ w-fu1l p-2 border rounded
$ferrors[field] ? "border-red-500":"border- green-400"))
/>
ferrors[field] 88 <p className="text-red- 500 text-sm">(errors[field]</p>)
</div>
)))
<button type=-"submit" className="w-ful1
bg-blue-600 text-hite py-2 rounded
hover:bg-blue-700">
Register
</button>
</form>
</div>
)；
import React from"react";
export default function SuccessMessage(f
message ))f
return(
<div className="bg-green-200 text-green
-800 p-2 rounded mb-4 text-center">
fmessage)
</div>
)；
import React from"react";
import FormValidation from
"./components/FormValidation";
function App()[
return <FormValidation />;
export default App;
module.exports =f
content:["./src/**/*.(js, jsx, ts, tsx"],theme:
f extend:0)，
plugins:[],
importReactfrom"react";
exportdefaultfunctionSuccessMessage
(f message))f
return(
<divclassName="bg-green-200text-
green -800p-2roundedmb-4text-center
">
fmessage)
</div>

