# VerifyMyAid
Give recipients a trusted way to verify aid messages, codes, or agents—and report scams—via SMS, WhatsApp, and web/app.
// This is a simplified clickable prototype using React and Tailwind for a "Verify My Aid" tool
// It includes:
// - Campaign lookup form
// - Code verification field
// - Mocked API responses

import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { CheckCircle, AlertCircle } from "lucide-react";

export default function VerifyMyAid() {
  const [code, setCode] = useState("");
  const [status, setStatus] = useState(null);
  const [campaign, setCampaign] = useState(null);

  const mockCampaigns = {
    "GD456ELN": {
      org: "GiveDirectly",
      region: "Zambezia, Mozambique",
      hotline: "+258 82 123 4567",
      start_date: "2025-07-20",
      end_date: "2025-09-30"
    },
    "GD-TEST-404": null
  };

  const handleVerify = () => {
    const result = mockCampaigns[code.trim()];
    setCampaign(result);
    setStatus(result ? "verified" : "not_found");
  };

  return (
    <div className="max-w-xl mx-auto mt-10 p-4 space-y-6">
      <h1 className="text-2xl font-bold text-center">Verify My Aid</h1>

      <Card>
        <CardContent className="p-4 space-y-4">
          <Input
            placeholder="Enter your verification code"
            value={code}
            onChange={(e) => setCode(e.target.value)}
          />
          <Button onClick={handleVerify}>Check Code</Button>

          {status === "verified" && campaign && (
            <div className="p-4 bg-green-100 rounded-lg">
              <div className="flex items-center gap-2 text-green-700">
                <CheckCircle className="w-5 h-5" />
                <span>✅ This aid offer is legitimate</span>
              </div>
              <ul className="mt-2 text-sm text-gray-700">
                <li><strong>Organization:</strong> {campaign.org}</li>
                <li><strong>Region:</strong> {campaign.region}</li>
                <li><strong>Hotline:</strong> {campaign.hotline}</li>
                <li><strong>Valid Dates:</strong> {campaign.start_date} – {campaign.end_date}</li>
              </ul>
            </div>
          )}

          {status === "not_found" && (
            <div className="p-4 bg-red-100 rounded-lg">
              <div className="flex items-center gap-2 text-red-700">
                <AlertCircle className="w-5 h-5" />
                <span>⚠️ Code not found. This message may be fraudulent.</span>
              </div>
              <p className="mt-2 text-sm text-gray-600">Please do not share your personal information. Call your local aid hotline to confirm.</p>
            </div>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
