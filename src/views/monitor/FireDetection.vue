<script setup>
  import { ref } from 'vue'
  const visibleScrollingLongContentDemo = ref(false)
</script>

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
                title="Read Alearts"
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
        <CCardHeader class="d-flex justify-content-between align-items-center">
          <strong>Recent Alerts</strong>
          <a href="#" class="text-decoration-none">View All</a>
        </CCardHeader>
        <CCardBody>
          <!-- Single aleart -->
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
                    src="C:\Users\intern.dppthinh\Desktop\webai-platform\coreui-free-vue-admin-template-main\src\assets\images\firedetection\Untitled.png"
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
                    src="C:\Users\intern.dppthinh\Desktop\webai-platform\coreui-free-vue-admin-template-main\src\assets\images\firedetection\Untitled.png"
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
                    src="C:\Users\intern.dppthinh\Desktop\webai-platform\coreui-free-vue-admin-template-main\src\assets\images\firedetection\Untitled.png"
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
                    src="C:\Users\intern.dppthinh\Desktop\webai-platform\coreui-free-vue-admin-template-main\src\assets\images\firedetection\Untitled.png"
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
      src="C:\Users\intern.dppthinh\Desktop\webai-platform\coreui-free-vue-admin-template-main\src\assets\images\firedetection\Untitled.png"
      alt="Default"
      class="img-fluid rounded shadow detected_img"
      style="aspect-ratio: 4 / 3; object-fit: cover; width: 100%;"
    />
  </CModalBody>
</CModal>

</template>





