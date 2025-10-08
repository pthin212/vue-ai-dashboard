<template>
  <CRow>
    <CCol>
      <!-- System Overview Section -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>System Overview</strong>
        </CCardHeader>
        <CCardBody>
          <!-- System statistics widgets row -->
          <CRow>
            <CCol sm="6" lg="3">
              <!-- Total cameras widget -->
              <CWidgetStatsA
                class="mb-4"
                color="primary"
                title="Total Cameras"
                :value="String(systemStats.total_cameras)"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <!-- Online cameras widget -->
              <CWidgetStatsA
                class="mb-4"
                color="success"
                title="Online Cameras"
                :value="String(systemStats.active_cameras)"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <!-- Total users widget -->
              <CWidgetStatsA
                class="mb-4"
                color="info"
                title="Total Users"
                :value="String(systemStats.total_users)"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <!-- Active users widget -->
              <CWidgetStatsA
                class="mb-4"
                color="warning"
                title="Active Users"
                :value="String(systemStats.active_users)"
              />
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>
      
      <!-- Alert Summary Section -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Alert Summary</strong>
        </CCardHeader>
        <CCardBody>
          <!-- Alert statistics widgets row -->
          <CRow>
            <CCol sm="6" lg="4">
              <!-- Total alerts widget -->
              <CWidgetStatsA
                class="mb-4"
                color="primary"
                title="Total Alerts"
                :value="String(+alertStats.total_alerts ?? 0)"
              />
            </CCol>
            <CCol sm="6" lg="4">
              <!-- Unread alerts widget -->
              <CWidgetStatsA
                class="mb-4"
                color="warning"
                title="Unread Alerts"
                :value="String(+alertStats.unread_alerts ?? 0)"
              />
            </CCol>
            <CCol sm="6" lg="4">
              <!-- Read alerts widget -->
              <CWidgetStatsA
                class="mb-4"
                color="success"
                title="Read Alerts"
                :value="String(+alertStats.read_alerts ?? 0)"
              />
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>

      <!-- Alerts by Type Section -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Alerts by Type</strong>
        </CCardHeader>
        <CCardBody>
          <!-- Scrollable table container -->
          <div style="max-height: 250px; overflow-y: auto;">
            <!-- Alert types breakdown table -->
            <CTable>
              <CTableHead>
                <CTableRow>
                  <!-- Sticky header columns -->
                  <CTableHeaderCell
                    style="position: sticky; top: 0;z-index: 1;"
                  >
                    Type
                  </CTableHeaderCell>
                  <CTableHeaderCell
                    style="position: sticky; top: 0; z-index: 1;"
                  >
                    Count
                  </CTableHeaderCell>
                  <CTableHeaderCell
                    style="position: sticky; top: 0; z-index: 1;"
                  >
                    Percentage
                  </CTableHeaderCell>
                </CTableRow>
              </CTableHead>
              <CTableBody>
                <!-- Loop through alert type statistics -->
                <CTableRow
                  v-for="(typeStat, index) in alertStats.total_alert_percentages"
                  :key="index"
                >
                  <CTableDataCell>
                    <!-- Alert type badge with dynamic styling -->
                    <CBadge :style="getBadgeStyle(typeStat.type)">
                      {{ typeStat.type }}
                    </CBadge>
                  </CTableDataCell>
                  <CTableDataCell>{{ typeStat.count }}</CTableDataCell>
                  <CTableDataCell>{{ typeStat.percentage }}%</CTableDataCell>
                </CTableRow>
              </CTableBody>
            </CTable>
          </div>
        </CCardBody>
      </CCard>

      <!-- Detection Feed Section -->
      <CCard class="mb-4">
        <CCardHeader class="d-flex justify-content-between align-items-center flex-wrap">
          <!-- Left: Title + Filters -->
          <div class="d-flex align-items-center gap-2 flex-wrap">
            <strong>Detection Feed</strong>
          </div>

          <!-- Right: View All link to clear camera selection -->
          <a href="#" class="text-decoration-none ms-auto" @click.prevent="clearSelectedCamera">View All</a>
        </CCardHeader>

        <CCardBody>
          <CRow>
            <!-- Left column: Camera list -->
            <CCol md="4" class="pe-3 border-end">
              <!-- Camera search input -->
              <CInputGroup class="mb-3">
                <CFormInput
                  v-model="cameraSearch"
                  placeholder="Search cameras..."
                  class="form-control-sm"
                />
              </CInputGroup>

              <!-- Scrollable camera list -->
              <div class="scroll-container m-0">
                <!-- Loop through filtered cameras -->
                <CRow
                  v-for="cam in filteredCameras"
                  :key="cam.id"
                  :class="selectedCameraId === cam.camera_id ? 'camgr-card-primary-effect' : 'camgr-card-hover-effect'"
                  class="py-1 mb-1"
                  @click="selectCamera(cam.id)"
                  style="cursor: pointer;"
                >
                  <CCol md="12">
                    <!-- Camera name and unread count -->
                    <div class="d-flex align-items-center gap-2">
                      <span class="fw-bold">{{ cam.name }}</span>
                      <span class="badge-rect">{{ cam.unread_detections }}</span>
                    </div>
                    <!-- Camera description with line breaks -->
                    <p v-html="cam.short_description.replace(/\|/g, '<br />')"></p>

                    <!-- Camera detail link -->
                    <a
                      href="#"
                      class="text-primary fw-semibold"
                      @click.prevent="openCameraDetail(cam)"
                    >
                      View details
                    </a>
                    &nbsp;
                    <!-- Google Maps link -->
                    <a
                      :href="`https://maps.google.com/?q=0,0`"
                      target="_blank"
                      class="text-primary fw-semibold"
                    >
                      View on Maps
                    </a>
                  </CCol>
                </CRow>
              </div>
            </CCol>

            <!-- Right column: Detection list -->
            <CCol md="8">
              <div class="scroll-container m-0 m-0">
                <!-- Single alert -->
                <CRow class="camgr-card-hover-effect py-1">
                  <CCol md="12">
                    <CRow>
                      <CCol md="8">
                        <CBadge color="warning">Dangerous Situation</CBadge>
                        <span class="fw-bold mx-2">Thinh's Camera</span>
                        <CBadge color="danger">New</CBadge>
                      </CCol>
                      <CCol md="4">
                        <CButton color="primary" variant="outline" class="ms-auto d-block my-1">Mark Read</CButton>
                      </CCol>
                    </CRow>
                    <CRow>
                      <CCol md="2">
                        <img
                          src=".\src\assets\images\firedetection\Untitled.png"
                          alt="Default"
                          class="img-fluid rounded shadow detected_img"
                          style="aspect-ratio: 4 / 3; object-fit: cover; width: 100%; max-width: 400px;"
                          title="Click to view details.."
                          @click="() => { visibleScrollingLongContentDemo = true }"
                        />
                      </CCol>
                      <CCol md="10">
                        <div class="text-muted small">2025-08-05 13:26:00</div>
                        <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View on Maps</a>
                      </CCol>
                    </CRow>
                  </CCol>
                </CRow>
                
                <!-- Whole things -->
                <CRow
                  v-for="(item, index) in detections"
                  :key="item.id"
                  class="camgr-card-hover-effect py-1"
                >
                  <CCol md="12">
                    <!-- Detection header row -->
                    <CRow>
                      <CCol md="8 mb-4">
                        <!-- Detection type badge -->
                        <CBadge :style="getBadgeStyle(item.type)">
                          {{ item.type }}
                        </CBadge>
                        <!-- Camera ID -->
                        <span class="fw-bold mx-2">{{ item.camera_id }}</span>
                        <!-- Seen/New status badge -->
                        <CBadge :color="item.seen ? 'secondary' : 'danger'">
                          {{ item.seen ? 'Seen' : 'New' }}
                        </CBadge>
                      </CCol>
                      <CCol md="4">
                        <!-- Mark as read button for unread detections -->
                        <CButton
                          v-if="!item.seen"
                          color="primary"
                          variant="outline"
                          class="ms-auto d-block my-1"
                          @click="markAsRead(item)"
                        >
                          Mark Read
                        </CButton>
                      </CCol>
                    </CRow>

                    <!-- Detection content row -->
                    <CRow>
                      <CCol md="2">
                        <!-- Detection image (clickable) -->
                        <img
                          :src="`data:image/png;base64,${item.base64}`"
                          alt="Detected"
                          class="img-fluid rounded shadow detected_img"
                          style="aspect-ratio: 4 / 3; object-fit: cover; width: 100%; max-width: 400px;"
                          title="Click to view details.."
                          @click="handleImageClick(item.base64)"
                        />
                      </CCol>
                      <CCol md="10">
                        <!-- Detection timestamp -->
                        <div class="text-muted small">{{ formatDate(item.timestamp) }}</div>
                        <!-- Google Maps link with coordinates -->
                        <a
                          :href="`https://maps.google.com/?q=${item.lat},${item.long}`"
                          target="_blank"
                          class="text-primary fw-semibold"
                        >
                          View on Maps
                        </a>
                      </CCol>
                    </CRow>
                  </CCol>
                </CRow>
              </div>
              <!-- Pagination controls -->
              <div class="d-flex justify-content-end mt-3">
                <CPagination align="end" size="sm">
                  <CPaginationItem
                    v-for="(item, index) in getPageItems"
                    :key="index"
                    :active="item === currentPage"
                    :disabled="item === '...'"
                    @click="item !== '...' && (currentPage = item)"
                    style="cursor: pointer"
                  >
                    {{ item }}
                  </CPaginationItem>
                </CPagination>
              </div>
              </div>
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>

      <!-- System Information Section -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Infrastructure Overview</strong>
        </CCardHeader>
        <CCardBody>
          <CRow>
            <!-- System details column -->
            <CCol md="6">
              <h5 class="mb-4">SYSTEM DETAILS</h5>
              <p><strong>Model:</strong> ShieldCam</p>
              <p><strong>Version:</strong> 2.1.4</p>
              <p><strong>Last Update:</strong> 2024-01-15 14:30:22</p>
              <p><strong>Uptime:</strong> 15 days, 8 hours, 32 minutes</p>
              <p><strong>Firmware Status:</strong> Up-to-date</p>
              <p><strong>Temperature Sensor:</strong> Normal</p>
              <p><strong>Power Supply:</strong> Stable</p>
            </CCol>
            <!-- Coverage area column -->
            <CCol md="6">
              <h5 class="mb-4">COVERAGE AREA</h5>
              <p><strong>Total Sensors:</strong> 24</p>
              <p><strong>Buildings Monitored:</strong> 3</p>
              <p><strong>Coverage Area:</strong> 15,000 sq ft</p>
              <p><strong>Response Time:</strong> &lt; 30 seconds</p>
              <p><strong>Zones Active:</strong> 12</p>
              <p><strong>Average Signal Strength:</strong> Good</p>
              <p><strong>Environmental Rating:</strong> IP67</p>
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>
    </CCol>
  </CRow>


<!-- Alert Image Modal -->
<CModal 
  :visible="visibleScrollingLongContentDemo"
  @close="() => { visibleScrollingLongContentDemo = false }"
  aria-labelledby="ScrollingLongContentExampleLabel"
>
  <CModalHeader>
  <CModalTitle id="ScrollingLongContentExampleLabel">Alert Image</CModalTitle>
  </CModalHeader>
  <CModalBody>
    <!-- Full-size detection image -->
    <img
      :src="'data:image/png;base64,' + selectedImage"
      alt="Default"
      class="img-fluid rounded shadow detected_img"
      style="aspect-ratio: 4 / 3; object-fit: cover; width: 100%;"
    />
  </CModalBody>
</CModal>


<!-- Camera Detail Modal -->
<CModal
  :visible="showCameraDetailModal"
  @close="() => { showCameraDetailModal = false }"
  alignment="center"
  size="lg"
>
  <CModalHeader>
    <CModalTitle>Camera Detail</CModalTitle>
  </CModalHeader>
  <CModalBody v-if="modalCamera">
    <!-- Camera image -->
    <div class="mb-1 text-center">
      <img
        :src="`data:image/png;base64,${modalCamera.base64}`"
        alt="Camera Image"
        class="img-fluid rounded shadow"
        style="max-height: 300px; object-fit: contain;"
      />
    </div>
    <!-- Camera information -->
    <div class="mb-1">
      <strong>ID:</strong> {{ modalCamera.camera_id }}
    </div>
    <div class="mb-1">
      <strong>Name:</strong> {{ modalCamera.name }}
    </div>
    <div>
      <strong>Description:</strong>
      <pre class="mt-2" style="white-space: pre-line">{{ modalCamera.details_description }}</pre>
    </div>
  </CModalBody>
</CModal>

</template>



<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import axios from 'axios'

// ========================================
// REACTIVE DATA DECLARATIONS
// ========================================

// Camera Management
const cameras = ref([])                          // List of all cameras
const selectedCameraId = ref(null)               // Currently selected camera ID
const cameraSearch = ref('')                     // Search keyword for filtering cameras
const showCameraDetailModal = ref(false)         // Camera detail modal visibility
const modalCamera = ref(null)                    // Camera data for detail modal

// Detection Management
const detections = ref([])                       // List of detections for current page
const currentPage = ref(1)                       // Current page number
const itemsPerPage = 6                          // Number of items per page
const totalDetections = ref(0)                   // Total number of detections
const loadingDetections = ref(false)             // Loading state for detections

// Image Modal Management
const visibleScrollingLongContentDemo = ref(false)  // Image modal visibility
const selectedImage = ref('')                    // Selected image data for modal

// Alert Statistics
const alertStats = ref({
  total_alerts: 0,
  unread_alerts: 0,
  read_alerts: 0,
  total_alert_percentages: [],                   // Array of alert type statistics
})

// System Statistics
const systemStats = ref({
  total_cameras: 0,
  active_cameras: 0,
  total_users: 0,
  active_users: 0,
})

// ========================================
// COMPUTED PROPERTIES
// ========================================

// Get currently selected camera object
const selectedCamera = computed(() =>
  cameras.value.find((cam) => cam.id === selectedCameraId.value)
)

// Filter cameras based on search keyword
const filteredCameras = computed(() => {
  if (!cameraSearch.value) return cameras.value
  const keyword = cameraSearch.value.toLowerCase()
  return cameras.value.filter((cam) =>
    cam.name.toLowerCase().includes(keyword) ||
    cam.short_description.toLowerCase().includes(keyword)
  )
})

// Calculate total number of pages for pagination
const totalPages = computed(() => Math.ceil(totalDetections.value / itemsPerPage))

// Generate pagination items with ellipsis logic
const getPageItems = computed(() => {
  const pages = []
  const delta = 2                                // Number of pages around current page

  // Show all pages if total is small
  if (totalPages.value <= 10) {
    for (let i = 1; i <= totalPages.value; i++) pages.push(i)
  } else {
    // Complex pagination with ellipsis
    pages.push(1)                               // Always show first page
    
    // Add ellipsis if current page is far from start
    if (currentPage.value > delta + 2) pages.push('...')
    
    // Calculate start and end of middle section
    const start = Math.max(2, currentPage.value - delta)
    const end = Math.min(totalPages.value - 1, currentPage.value + delta)
    
    // Add middle pages
    for (let i = start; i <= end; i++) pages.push(i)
    
    // Add ellipsis if current page is far from end
    if (currentPage.value < totalPages.value - delta - 1) pages.push('...')
    
    // Always show last page
    pages.push(totalPages.value)
  }

  return pages
})

// ========================================
// WATCHERS
// ========================================

// Watch for changes in selected camera or current page to refetch detections
watch([selectedCameraId, currentPage], () => {
  fetchDetections()
})

// ========================================
// API FUNCTIONS
// ========================================

// Fetch all cameras from API
async function fetchCameras() {
  try {
    const res = await axios.get('http://192.168.189.153:8000/ai/cameras?skip=0&limit=100')
    cameras.value = res.data
  } catch (err) {
    console.error('Failed to fetch cameras:', err)
  }
}

// Fetch detections from API with pagination and filtering
async function fetchDetections() {
  try {
    loadingDetections.value = true
    const skip = (currentPage.value - 1) * itemsPerPage
    const params = {
      skip,
      limit: itemsPerPage,
    }

    // Add camera filter if a camera is selected
    if (selectedCameraId.value) {
      params.camera_id = String(selectedCameraId.value)
    }

    const res = await axios.get('http://192.168.189.153:8000/ai/detections', {
      params,
    })

    detections.value = res.data.detections
    totalDetections.value = res.data.total
  } catch (err) {
    console.error('Error fetching detections:', err)
  } finally {
    loadingDetections.value = false
  }
}

// Fetch alert statistics from API
async function fetchAlertStatistics() {
  try {
    const res = await axios.get('http://192.168.189.153:8000/ai/alerts/statistics')
    alertStats.value = res.data
  } catch (err) {
    console.error('Failed to fetch alert statistics:', err)
  }
}

// Fetch system statistics from multiple API endpoints
async function fetchSystemStats() {
  try {
    // Parallel API calls for camera and user statistics
    const [cameraRes, userRes] = await Promise.all([
      axios.get('http://192.168.189.153:8000/ai/cameras/summary'),
      axios.get('http://192.168.189.153:8000/ai/users/summary'),
    ])

    // Update system statistics with API response data
    systemStats.value.total_cameras = cameraRes.data.total_cameras
    systemStats.value.active_cameras = cameraRes.data.active_cameras
    systemStats.value.total_users = userRes.data.total_users
    systemStats.value.active_users = userRes.data.active_users
  } catch (err) {
    console.error('Failed to fetch system stats:', err)
  }
}

// Mark detection as read/seen
async function markAsRead(item) {
  try {
    const detectionId = item.id
    // Send PATCH request to mark detection as seen
    await axios.patch(
      `http://192.168.189.153:8000/ai/detections/${detectionId}/seen`,
      true,
      {
        headers: {
          'Content-Type': 'application/json',
        },
      }
    )

    // Refresh data after marking as read
    await fetchDetections()                      // Refresh detection list
    await fetchCameras()                         // Refresh camera list (updates unread counts)
    await fetchAlertStatistics()                 // Refresh alert statistics
  } catch (err) {
    console.error('Failed to mark detection as read:', err)
  }
}

// ========================================
// USER INTERACTION FUNCTIONS
// ========================================

// Select a camera by object ID
function selectCamera(objectId) {
  const camera = cameras.value.find(c => c.id === objectId)
  if (camera) {
    selectedCameraId.value = camera.camera_id
    currentPage.value = 1                        // Reset to first page when selecting camera
  }
}

// Clear camera selection to show all detections
function clearSelectedCamera() {
  selectedCameraId.value = null
  currentPage.value = 1                          // Reset to first page
}

// Open camera detail modal
function openCameraDetail(camera) {
  modalCamera.value = camera
  showCameraDetailModal.value = true
}

// Handle click on detection image to open modal
function handleImageClick(base64) {
  selectedImage.value = base64
  visibleScrollingLongContentDemo.value = true
}

// ========================================
// UTILITY FUNCTIONS
// ========================================

// Format datetime string to Vietnamese locale
function formatDate(datetimeStr) {
  const date = new Date(datetimeStr)
  return date.toLocaleString('vi-VN', {
    year: 'numeric',
    month: '2-digit',
    day: '2-digit',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
  })
}

// Get badge style object with background and text color
function getBadgeStyle(type) {
  const bg = getBadgeColor(type)
  const color = getTextColor(bg)
  return {
    backgroundColor: bg,
    color: color,
  }
}

// Get badge background color based on alert type
function getBadgeColor(type) {
  if (!type) return '#6c757d'                    // gray for undefined type

  const lower = type.toLowerCase()

  // Special colors for specific alert types
  if (lower === 'sos') return '#dc3545'          // red for SOS
  if (lower === 'ds' || lower === 'dangerous situation') return '#ffc107'  // yellow for dangerous situation

  // Generate distinct color for other types
  return stringToDistinctColor(lower)
}

// Generate distinct color from string using hash
function stringToDistinctColor(str) {
  let hash = 0
  // Calculate hash from string characters
  for (let i = 0; i < str.length; i++) {
    hash = str.charCodeAt(i) + ((hash << 5) - hash)
  }

  // Use hash to pick hue between 0-360 with additional randomization
  const hue = Math.abs(hash) % 360 + Math.abs(hash) % 31
  const saturation = 90                          // High saturation for vibrant colors
  const value = 90                              // High brightness

  return hsvToHex(hue, saturation, value)
}

// Convert HSV color values to hexadecimal
function hsvToHex(h, s, v) {
  s /= 100
  v /= 100

  const c = v * s
  const x = c * (1 - Math.abs((h / 60) % 2 - 1))
  const m = v - c

  let r = 0, g = 0, b = 0

  // Determine RGB values based on hue
  if (0 <= h && h < 60) [r, g, b] = [c, x, 0]
  else if (60 <= h && h < 120) [r, g, b] = [x, c, 0]
  else if (120 <= h && h < 180) [r, g, b] = [0, c, x]
  else if (180 <= h && h < 240) [r, g, b] = [0, x, c]
  else if (240 <= h && h < 300) [r, g, b] = [x, 0, c]
  else if (300 <= h && h < 360) [r, g, b] = [c, 0, x]

  // Convert to 0-255 range
  r = Math.round((r + m) * 255)
  g = Math.round((g + m) * 255)
  b = Math.round((b + m) * 255)

  // Convert to hex string
  const toHex = (n) => n.toString(16).padStart(2, '0')
  return `#${toHex(r)}${toHex(g)}${toHex(b)}`
}

// Determine text color (black/white) based on background brightness
function getTextColor(bgColor) {
  // Extract RGB values from hex color
  const r = parseInt(bgColor.slice(1, 3), 16)
  const g = parseInt(bgColor.slice(3, 5), 16)
  const b = parseInt(bgColor.slice(5, 7), 16)
  
  // Calculate brightness using weighted formula
  const brightness = (r * 299 + g * 587 + b * 114) / 1000
  
  // Return black for bright backgrounds, white for dark backgrounds
  return brightness > 140 ? '#000000' : '#ffffff'
}

// ========================================
// COMPONENT LIFECYCLE
// ========================================

// Execute when component is mounted
onMounted(() => {
  fetchCameras()                                 // Load camera list
  fetchDetections()                              // Load initial detections
  fetchAlertStatistics()                         // Load alert statistics
  fetchSystemStats()                             // Load system statistics
})
</script>