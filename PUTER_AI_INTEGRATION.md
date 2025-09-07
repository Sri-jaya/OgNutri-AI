# Puter AI Integration

This project now supports both Google Gemini and GPT-4 (via Puter AI) for AI-powered medical support and food recommendations.

## Features

### AI Model Selection

- **Google Gemini**: Default AI model using Google's Gemini 2.0 Flash
- **GPT-4 via Puter**: Alternative AI model using OpenAI's GPT-4 through Puter's AI service

### Supported Pages

1. **Medical Support** (`/dashboard/medical-support`)

   - Find nearby medical facilities and specialists
   - Get structured recommendations with medical reports support
   - Select up to 2 medical reports per request

2. **Food Recommendations** (`/dashboard/food-recommendations`)
   - Get personalized organic food suggestions
   - Structured JSON responses with categorized recommendations
   - Dietary preferences and health condition considerations

## How to Use

1. **Select AI Model**: Choose between "Google Gemini (Default)" or "GPT-4 via Puter" in the dropdown
2. **Fill Form**: Complete location, health conditions, and optional notes
3. **Add Reports** (Medical Support only): Select up to 2 relevant medical reports
4. **Get Recommendations**: Submit the form to receive AI-powered suggestions

## Technical Implementation

### New Files

- `/src/ai/flows/find-nearby-medical-support-puter.ts` - Puter AI medical support flow
- `/src/ai/flows/get-organic-food-recommendations-puter.ts` - Puter AI food recommendations flow

### Key Features

- **Automatic SDK Loading**: Puter SDK loads automatically when page loads
- **Graceful Fallback**: Falls back to structured responses if JSON parsing fails
- **History Tracking**: Shows which AI model was used for each request
- **Error Handling**: Clear error messages for each AI service

### API Models Used

- **Puter AI**: `gpt-4o-mini` model for both medical and food recommendations
- **Gemini**: `googleai/gemini-2.0-flash` model (existing implementation)

## Response Formats

### Medical Support (Structured JSON)

```json
{
  "immediateActions": ["action1", "action2"],
  "recommendedFacilities": [
    {
      "name": "Facility Name",
      "type": "Hospital/Clinic",
      "relevance": "Why relevant",
      "contact": "Phone/website"
    }
  ],
  "relevantSpecialists": [
    {
      "specialty": "Specialist type",
      "relevance": "Why relevant"
    }
  ],
  "supportResources": ["Support groups", "Helplines"],
  "selfMonitoring": ["What to track", "Documents to bring"],
  "urgentCareWarnings": ["Warning signs"]
}
```

### Food Recommendations (Structured JSON)

```json
{
  "Key Nutritional Priorities": ["priority1", "priority2"],
  "Recommended Organic Foods": {
    "Vegetables": [{ "item": "name", "rationale": "why beneficial" }],
    "Fruits": [{ "item": "name", "rationale": "why beneficial" }]
    // ... other categories
  },
  "Sample 1-Day Meal Outline": {
    "Breakfast": "meal description",
    "Lunch": "meal description"
    // ... other meals
  },
  "Seasonal & Local Suggestions": ["suggestion1", "suggestion2"],
  "Cautions / Foods to Limit": [{ "item": "food", "rationale": "why limit" }]
}
```

## Benefits of Dual AI Support

1. **Model Comparison**: Users can compare responses from different AI models
2. **Reliability**: Backup option if one service is unavailable
3. **Specialized Strengths**: Different models may excel in different areas
4. **User Choice**: Flexibility to choose preferred AI provider

## Development Notes

- Puter flows are client-side components (`'use client'`)
- Gemini flows remain server-side components (`'use server'`)
- Both implementations maintain the same input/output schemas for consistency
- History entries track which AI model was used for future reference
