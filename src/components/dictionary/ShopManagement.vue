<template>
  <div>
    <div class="right-content">
      <div class="right-content-grid">
        <div class="remote-container">
          <div
            class="button-remote button-addCustomer"
            style="display: flex"
            @click="show"
          >
            <span
              data-ref="btnIconEl"
              role="presentation"
              unselectable="on"
              class="x-btn-icon icon-insert"
              style=""
            ></span>
            <div class="r-button boder-right">Thêm mới</div>
          </div>
          <div class="button-remote r-button boder-right">
            <span
              data-ref="btnIconEl"
              role="presentation"
              unselectable="on"
              class="x-btn-icon icon-btnclone"
              style=""
            ></span>
            <div class="text">Nhân bản</div>
          </div>
          <div class="button-remote" style="display: flex">
            <span
              data-ref="btnIconEl"
              role="presentation"
              unselectable="on"
              class="x-btn-icon icon-update"
              style=""
            ></span>
            <div class="r-button boder-right" style="display: flex">Sửa</div>
          </div>

          <div class="button-remote" style="display: flex">
            <span
              data-ref="btnIconEl"
              role="presentation"
              unselectable="on"
              class="x-btn-icon icon-delete"
              style=""
            ></span>
            <div class="r-button boder-right">Xóa</div>
          </div>
          <div class="button-remote" style="display: flex">
            <span
              data-ref="btnIconEl"
              role="presentation"
              unselectable="on"
              class="x-btn-icon icon-refresh"
              style=""
            ></span>
            <div class="r-button">Nạp</div>
          </div>
        </div>
        <div class="x-panel">
          <div class="x-grid-table">
            <div class="x-grid-header">
              <div class="x-column-header column-storeid">
                <div class="x-column-header-inner">
                  <div class="x-fontw column-name">Mã cửa hàng</div>
                </div>
                <div class="x-column-header-condition">
                  <a href="" class="condition-btn"></a>
                  <div class="condition-text"></div>
                </div>
              </div>
              <div class="x-column-header column-storename">
                <div class="x-column-header-inner">
                  <div class="x-fontw column-name">Tên cửa hàng</div>
                </div>
                <div class="x-column-header-condition">
                  <a href="" class="condition-btn"></a>
                  <div class="condition-text"></div>
                </div>
              </div>
              <div class="x-column-header column-storeaddress">
                <div class="x-column-header-inner">
                  <div class="x-fontw column-name">Địa chỉ</div>
                </div>
                <div class="x-column-header-condition">
                  <a href="" class="condition-btn"></a>
                  <div class="condition-text"></div>
                </div>
              </div>
              <div class="x-column-header column-storenumber">
                <div class="x-column-header-inner">
                  <div class="x-fontw column-name">Số điện thoại</div>
                </div>
                <div class="x-column-header-condition">
                  <a href="" class="condition-btn"></a>
                  <div class="condition-text"></div>
                </div>
              </div>
              <div class="x-column-header column-storestatus">
                <div class="x-column-header-inner">
                  <div class="x-fontw column-name">Trạng thái</div>
                </div>
                <div class="x-column-header-condition">
                  <div class="condition-text" style="margin-left: 2px"></div>
                </div>
              </div>
            </div>
            <div class="x-grid-body">
              <table cellpadding="0" cellspacing="0">
                <thead>
                  <tr>
                    <th class="th-storeid"></th>
                    <th class="th-storename"></th>
                    <th class="th-storeaddress"></th>
                    <th class="th-storenumber"></th>
                    <th class="th-storestatus"></th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                    v-for="shop in stores"
                    :key="shop.storeId"
                    @dblclick="showDetail(shop)"
                  >
                    <td>{{ shop.storeCode }}</td>
                    <td>{{ shop.storeName }}</td>
                    <td>{{ shop.address }}</td>
                    <td>{{ shop.phoneNumber }}</td>
                    <td>đang hoạt động</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          <div class="x-grid-footer toolbar">
            <div class="paging-toolbar">
              <div class="leftchild">
                <div class="p-button first-page"></div>
                <div class="p-button prev-page"></div>
                <div style="margin: 0 16px 0 4px">Trang</div>
                <input type="text" value="1" class="text-pagebumber" />
                <div style="margin: 0 16px 0 6px">Trên 1</div>

                <div class="p-button next-page"></div>
                <div class="p-button last-page"></div>
                <div class="p-button refresh"></div>
                <select name="" id="" class="select-quantitypage">
                  <option value="">25</option>
                  <option value="">50</option>
                  <option value="">100</option>
                </select>
              </div>
              <div class="rightchild">
                <div class="noticenuber-paging">
                  Hiển thị 1 - 6 trên 6 kết quả
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <ShopModalCreate ref="ShopModalCreate_ref" :store="store" :formMode="formMode" />
  </div>
</template>

<script>
import ShopModalCreate from "../modal/ShopManagement/ShopModalCreate.vue";
import axios from "axios";

export default {
  components: {
    ShopModalCreate,
  },
  methods: {
    // lấy dữ liệu các bản ghi shop
    getdata() {
      axios.get("http://localhost:35480/api/v1/Stores").then((Response) => {
        this.stores = Response.data.data;
      });
    },

    // hiển thị chi tiết bản ghi trên modal
    showDetail: async function (shop) {
      await ((this.store.storeCode = shop.storeCode),
      (this.store.storeName = shop.storeName),
      (this.store.address = shop.address),
      (this.store.phoneNumber = shop.phoneNumber),
      (this.store.storeTaxCode = shop.storeTaxCode),
      (this.store.countryId = shop.countryId),
      (this.store.wardId = shop.wardId),
      (this.store.provinceId = shop.provinceId),
      (this.store.districtId = shop.districtId)
      );

      this.$refs.ShopModalCreate_ref.showEditDialog();
      this.formMode = 'edit'
      // this.$refs.selectedCountry = this.store.countryId;
      // this.$refs.selectedCity = this.store.provinceId;
    },

    // reset lại input trong modal
    resetInput() {
      (this.store.storeCode = ""),
        (this.store.storeName = ""),
        (this.store.address = ""),
        (this.store.phoneNumber = ""),
        (this.store.storeTaxCode = "")
    },

    show() {
      this.$refs.ShopModalCreate_ref.showAddDialog();
      this.formMode = 'add'
      this.resetInput();
    },
  },
  data() {
    return {
      stores: [],
      store: {
        storeName: "",
        storeTaxCode: "",
        phoneNumber: "",
        address: "",
        storeCode: "",
        countryId: "",
        provinceId: "",
        districtId: "",
        wardId: "",
      },
      formMode:'add'
    };
  },
  created() {
    this.getdata();
  },
};
</script>

<style src="../../style/page/ShopManagement.scss" lang="scss"/>

<style scoped>
</style>