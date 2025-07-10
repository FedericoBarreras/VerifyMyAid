import React, { useState } from 'react';
import { CheckCircleIcon, ExclamationCircleIcon } from '@heroicons/react/solid'; // Optional: You can replace or remove

const VerifyMyAid = () => {
  const [code, setCode] = useState('');
  const [status, setStatus] = useState(null);
  const [campaign, setCampaign] = useState(null);

  const mockCampaigns = {
    'GD456ELN': {
      org: 'GiveDirectly',
      region: 'Zambezia, Mozambique',
      hotline: '+258 82 123 4567',
      start_date: '2025-07-20',
      end_date: '2025-09-30'
    },
    'GD123TEST': {
      org: 'ReliefOrg',
      region: 'Kerala, India',
      hotline: '+91 90000 00000',
      start_date: '2025-08-01',
      end_date: '2025-09-10'
    }
  };

  const handleVerify = () => {
    const result = mockCampaigns[code.trim()];
    setCampaign(result);
    setStatus(result ? 'verified' : 'not_found');
  };

  return (
    <div className="max-w-lg mx-auto mt-12 px-6 py-8 border rounded-lg shadow-md bg-white">
      <h2 className="text-2xl font-bold text-center mb-4">Verify My Aid</h2>
      
      <div className="space-y-4">
        <input
          type="text"
          placeholder="Enter your verification code"
          className="w-full border border-gray-300 p-2 rounded"
          value={code}
          onChange={(e) => setCode(e.target.value)}
        />
        <button
