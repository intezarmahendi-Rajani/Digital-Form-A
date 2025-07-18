# Digital-Form-A
For Utkal C Coal Mine of Jindal Steel and Power Ltd digital Form A for Mining employees as per 12th safety conference of DGMS.
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Label } from "@/components/ui/label";
import { Textarea } from "@/components/ui/textarea";

function LoginPage({ onLogin }) {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");

  const handleLogin = () => {
    if (username === "admin" && password === "admin") {
      onLogin();
    } else {
      alert("Invalid credentials");
    }
  };

  return (
    <div className="p-6 max-w-md mx-auto">
      <h1 className="text-xl font-bold mb-4">Login</h1>
      <div className="mb-2">
        <Label htmlFor="username">Username</Label>
        <Input id="username" value={username} onChange={e => setUsername(e.target.value)} />
      </div>
      <div className="mb-4">
        <Label htmlFor="password">Password</Label>
        <Input type="password" id="password" value={password} onChange={e => setPassword(e.target.value)} />
      </div>
      <Button onClick={handleLogin}>Login</Button>
    </div>
  );
}

function Dashboard() {
  return (
    <div className="p-6 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">Digital Form-A Dashboard</h1>
      <Card className="mb-4">
        <CardContent className="grid gap-4">
          <div>
            <Label htmlFor="employeeId">Employee ID</Label>
            <Input id="employeeId" placeholder="Enter Employee ID" />
          </div>
          <div>
            <Label htmlFor="name">Name</Label>
            <Input id="name" placeholder="Enter Name" />
          </div>
          <div>
            <Label htmlFor="designation">Designation</Label>
            <Input id="designation" placeholder="Enter Designation" />
          </div>
          <div>
            <Label htmlFor="department">Department</Label>
            <Input id="department" placeholder="Enter Department" />
          </div>
          <div>
            <Label htmlFor="vtDate">VT/PME Date</Label>
            <Input type="date" id="vtDate" />
          </div>
          <div>
            <Label htmlFor="expiryDate">Expiry Date</Label>
            <Input type="date" id="expiryDate" />
          </div>
          <div>
            <Label htmlFor="upload">Upload Medical/VT Report</Label>
            <Input type="file" id="upload" />
          </div>
          <div>
            <Label htmlFor="remarks">Remarks</Label>
            <Textarea id="remarks" placeholder="Add any notes or observations..." />
          </div>
          <Button className="mt-4 w-full">Submit</Button>
        </CardContent>
      </Card>
    </div>
  );
}

export default function DigitalFormAApp() {
  const [loggedIn, setLoggedIn] = useState(false);

  return loggedIn ? <Dashboard /> : <LoginPage onLogin={() => setLoggedIn(true)} />;
}
