# ⚡ Incidents API

The Incidents API allows you to record, read, update, and delete specific migraine events.

---

## 🟢 Create a New Incident

Records a new migraine incident for the authenticated user. This will automatically trigger the `Pattern Guardian` engine in the background to look for new predictive correlations.

**Endpoint:** `POST /incidents`  
**Auth Required:** Yes (`Bearer Token`)

### Request Body

The body must be a JSON object containing the incident details.

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `timestamp` | `string (ISO 8601)` | **Yes** | The exact date and time the incident started. |
| `severity` | `number` | **Yes** | Pain scale from 1 (mild) to 10 (severe). |
| `incidentType` | `string` | **Yes** | e.g., `"MIGRAINE"`, `"TENSION"`, `"CLUSTER"`. |
| `symptoms` | `array of strings` | No | IDs of symptoms experienced (e.g., aura, nausea). |
| `medications` | `array of strings` | No | IDs of rescue medications taken during the incident. |
| `durationHours` | `number` | No | The total length of the incident in hours. |

**Example Request:**

```json
{
  "timestamp": "2026-03-08T14:30:00Z",
  "severity": 8,
  "incidentType": "MIGRAINE",
  "symptoms": ["aura_id_123", "nausea_id_456"],
  "medications": ["sumatriptan_id_789"],
  "durationHours": 4.5
}
```

### Response

Returns the newly created incident object, including the assigned database ID and automatically attached environmental data (if available).

Status: `201 Created`

```json
{
  "id": "inc_987654321",
  "userId": "usr_123456",
  "timestamp": "2026-03-08T14:30:00Z",
  "severity": 8,
  "incidentType": "MIGRAINE",
  "symptoms": ["aura_id_123", "nausea_id_456"],
  "medications": ["sumatriptan_id_789"],
  "durationHours": 4.5,
  "environmentalSnapshot": {
    "barometricPressure": 1008,
    "uvIndex": 6,
    "kIndex": 3
  },
  "createdAt": "2026-03-08T18:45:00Z"
}
```

## 🔵 Get Recent Incidents

Retrieves a paginated list of the user's logged incidents.

**Endpoint:** `GET /incidents`
**Auth Required:** Yes (Bearer Token)

### Query Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `limit` | `number` | **No** | Number of records to return (Default: 10, Max: 50). |
| `page` | `number` | **No** | The page number for pagination (Default: 1). |
| `startDate` | `string` | **No** | Filter incidents starting after this ISO date. |

**Example Request:** `GET /incidents?limit=5&page=1`

### Response

Status: `200 OK`

```json
{
  "data": [
    {
      "id": "inc_987654321",
      "severity": 8,
      "incidentType": "MIGRAINE",
      "timestamp": "2026-03-08T14:30:00Z"
    }
  ],
  "meta": {
    "total": 14,
    "page": 1,
    "limit": 5
  }
}
```