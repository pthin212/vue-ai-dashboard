<!-- <script setup>
  import { ref } from 'vue'
  const visibleScrollingLongContentDemo = ref(false)
</script> -->

<template>
  <CRow>
    <CCol>

      <!-- System Overview -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>System Overview</strong>
        </CCardHeader>
        <CCardBody>
          <CRow>
            <CCol sm="6" lg="3">
              <CWidgetStatsA
                class="mb-4"
                color="primary"
                title="Total Cameras"
                value="2"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <CWidgetStatsA
                class="mb-4"
                color="success"
                title="Online Cameras"
                value="2"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <CWidgetStatsA
                class="mb-4"
                color="info"
                title="Total Users"
                value="1"
              />
            </CCol>
            <CCol sm="6" lg="3">
              <CWidgetStatsA
                class="mb-4"
                color="warning"
                title="Active Users"
                value="1"
              />
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>
      
      <!-- Alert Summary -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Alert Summary</strong>
        </CCardHeader>
        <CCardBody>
          <CRow>
            <CCol sm="6" lg="4">
              <CWidgetStatsA
                class="mb-4"
                color="primary"
                title="Total Alerts"
                value="19"
              />
            </CCol>
            <CCol sm="6" lg="4">
              <CWidgetStatsA
                class="mb-4"
                color="warning"
                title="Unread Alerts"
                value="10"
              />
            </CCol>
            <CCol sm="6" lg="4">
              <CWidgetStatsA
                class="mb-4"
                color="success"
                title="Read Alerts"
                value="9"
              />
            </CCol>
          </CRow>
        </CCardBody>
      </CCard>

      <!-- Alerts by Type -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>Alerts by Type</strong>
        </CCardHeader>
        <CCardBody>
          <CTable>
            <CTableHead>
              <CTableRow>
                <CTableHeaderCell>Type</CTableHeaderCell>
                <CTableHeaderCell>Count</CTableHeaderCell>
                <CTableHeaderCell>Percentage</CTableHeaderCell>
              </CTableRow>
            </CTableHead>
            <CTableBody>
              <CTableRow>
                <CTableDataCell>
                  <CBadge color="danger">SOS</CBadge>
                </CTableDataCell>
                <CTableDataCell>14</CTableDataCell>
                <CTableDataCell>73.7%</CTableDataCell>
              </CTableRow>
              <CTableRow>
                <CTableDataCell>
                  <CBadge color="warning">Dangerous Situation</CBadge>
                </CTableDataCell>
                <CTableDataCell>5</CTableDataCell>
                <CTableDataCell>26.3%</CTableDataCell>
              </CTableRow>
            </CTableBody>
          </CTable>
        </CCardBody>
      </CCard>

      <!-- Recent Alerts -->
      <CCard class="mb-4">
        <CCardHeader class="d-flex justify-content-between align-items-center flex-wrap">
          <!-- Left: Title + Filters -->
          <div class="d-flex align-items-center gap-2 flex-wrap">
            <strong>Recent Alerts</strong>
            <CFormSelect
              v-model="selectedType"
              :options="['All User', 'user1', 'user2']"
              class="form-select-sm"
              style="width: auto"
            />
          </div>

          <!-- Right: View All -->
          <a href="#" class="text-decoration-none ms-auto">View All</a>
        </CCardHeader>

        <CCardBody>
          <CRow>
            <CCol md="4" class="pe-3 border-end">
              <CInputGroup class="mb-3">
                <CFormInput
                  v-model="cameraSearch"
                  placeholder="Search cameras..."
                  class="form-control-sm"
                />
              </CInputGroup>

              <div class="scroll-container m-0 m-0">
                <CRow class="camgr-card-primary-effect py-1 mb-1">
                  <CCol md="12">
                    <span class="fw-bold">Thinh's Camera</span>
                    <br></br>
                    <p>
                      Model: AI-Cam X512<br />
                      Field of View: 110° (Horizontal)<br />
                    </p>
                    
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View details</a>
                    &nbsp;
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View on Maps</a>
                  </CCol>
                </CRow>

                <CRow class="camgr-card-hover-effect py-1 mb-1">
                  <CCol md="12">
                    <span class="fw-bold">Thinh's Camera</span>
                    <br></br>
                    <p>
                      Model: AI-Cam X512<br />
                      Field of View: 110° (Horizontal)<br />
                    </p>
                    
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View details</a>
                    &nbsp;
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View on Maps</a>
                  </CCol>
                </CRow>

                <CRow class="camgr-card-hover-effect py-1 mb-1">
                  <CCol md="12">
                    <span class="fw-bold">Thinh's Camera</span>
                    <br></br>
                    <p>
                      Model: AI-Cam X512<br />
                      Field of View: 110° (Horizontal)<br />
                    </p>
                    
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View details</a>
                    &nbsp;
                    <a href="https://maps.google.com" target="_blank" class="text-primary fw-semibold">View on Maps</a>
                  </CCol>
                </CRow>
              </div>
            </CCol>

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
                    <CRow>
                      <CCol md="8">
                        <CBadge :color="getBadgeColor(item.type)">
                          {{ item.type }}
                        </CBadge>
                        <span class="fw-bold mx-2">{{ item.camera_id }}</span>
                        <CBadge :color="item.seen ? 'secondary' : 'danger'">
                          {{ item.seen ? 'Seen' : 'New' }}
                        </CBadge>
                      </CCol>
                      <CCol md="4">
                        <CButton
                          color="primary"
                          variant="outline"
                          class="ms-auto d-block my-1"
                          @click="item.seen = true"
                        >
                          Mark Read
                        </CButton>
                      </CCol>
                    </CRow>

                    <CRow>
                      <CCol md="2">
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
                        <div class="text-muted small">{{ formatDate(item.timestamp) }}</div>
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
              <div class="d-flex justify-content-end mt-3">
                <CPagination align="end" size="sm">
                  <CPaginationItem
                    v-for="(item, index) in getPageItems"
                    :key="index"
                    :active="item === currentPage"
                    :disabled="item === '...'"
                    @click="item !== '...' && (currentPage = item)"
                  >
                    {{ item }}
                  </CPaginationItem>
                </CPagination>
              </div>
            </CCol>
          </CRow>
          

        </CCardBody>
      </CCard>

      <!-- System Information -->
      <CCard class="mb-4">
        <CCardHeader>
          <strong>System Information</strong>
        </CCardHeader>
        <CCardBody>
          <CRow>
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


<CModal 
  :visible="visibleScrollingLongContentDemo"
  @close="() => { visibleScrollingLongContentDemo = false }"
  aria-labelledby="ScrollingLongContentExampleLabel"
>
  <CModalHeader>
  <CModalTitle id="ScrollingLongContentExampleLabel">Alert Image</CModalTitle>
  </CModalHeader>
  <CModalBody>
    <img
      :src="'data:image/png;base64,' + selectedImage"
      alt="Default"
      class="img-fluid rounded shadow detected_img"
      style="aspect-ratio: 4 / 3; object-fit: cover; width: 100%;"
    />
  </CModalBody>
</CModal>

</template>





<script setup>
import { ref, onMounted, computed } from 'vue'
import axios from 'axios'

const detections = ref([])
const visibleScrollingLongContentDemo = ref(false)
const selectedImage = ref('')


onMounted(async () => {
  try {
    const response = await axios.get('http://192.168.189.153:8000/ai/detections')
    detections.value = response.data
    console.log('Dữ liệu API trả về:', detections.value)
  } catch (error) {
    console.error('Error fetching detections:', error)
  }
})

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

function getBadgeColor(type) {
  if (!type) return 'secondary'
  const lower = type.toLowerCase()
  if (lower === 'sos') return 'danger'
  if (lower === 'ds' || lower === 'dangerous situation') return 'warning'
  return 'info' // fallback
}

function handleImageClick(base64) {
  selectedImage.value = base64
  visibleScrollingLongContentDemo.value = true
}






const currentPage = ref(50) // Trang đang chọn (giả lập)
const totalPages = 100      // Tổng số trang

const getPageItems = computed(() => {
  const pages = []
  const delta = 2

  if (totalPages <= 10) {
    for (let i = 1; i <= totalPages; i++) pages.push(i)
  } else {
    pages.push(1)

    if (currentPage.value > delta + 2) {
      pages.push('...')
    }

    const start = Math.max(2, currentPage.value - delta)
    const end = Math.min(totalPages - 1, currentPage.value + delta)

    for (let i = start; i <= end; i++) pages.push(i)

    if (currentPage.value < totalPages - delta - 1) {
      pages.push('...')
    }

    pages.push(totalPages)
  }

  return pages
})
</script>