<template>
  <div>
    <div class="hello">
      <BaseModal ref="BaseModal_ref">
        <div class="header-dialog">
          <div class="header-title">Thêm mới cửa hàng</div>
          <div class="btn-close"></div>
        </div>
        <div class="body-dialog">
          <form action="#">
            <div class="dialog-content-top">
              <div class="input-row">
                <div class="ip-info-1">
                  <div class="label">Mã cửa hàng <span>*</span></div>
                  <input
                    type="text"
                    id="CustomerCode"
                    fieldName="CustomerCode"
                    class="m-input"
                    required
                    ref="input_1"
                    v-model="store.storeCode"
                    @blur="ValidateEmty('input_1')"
                    @keyup="ValidateEmty('input_1')"
                  />
                  <!-- <ModalValidata
                    ref="ModalValidata_ref"
                    :validate="validateBag"
                    color="red"
                  /> -->
                </div>
              </div>
              <div class="input-row">
                <div class="ip-info-1">
                  <div class="label">Tên cửa hàng <span>*</span></div>
                  <input
                    type="text"
                    id="CustomerName"
                    fieldName="FullName"
                    name="Customer-name"
                    class="m-input"
                    required
                    ref="input_2"
                    v-model="store.storeName"
                    @blur="ValidateEmty('input_2')"
                    @keyup="ValidateEmty('input_2')"
                  />
                </div>
                <div class="input-row"></div>
              </div>
              <div class="input-row">
                <div class="ip-info-1">
                  <div class="label lb-address">Địa chỉ <span>*</span></div>
                  <textarea
                    class="area-address"
                    aria-hidden="false"
                    aria-disabled="false"
                    aria-multiline="true"
                    role="textbox"
                    v-model="store.address"
                    required
                    aria-invalid="false"
                    aria-readonly="false"
                    aria-describedby="MISATextAreaField-1221-ariaStatusEl"
                    aria-required="true"
                    autocomplete="off"
                    data-componentid="MISATextAreaField-1221"
                    ref="input_3"
                    @blur="ValidateEmty('input_3')"
                    @keyup="ValidateEmty('input_3')"
                  ></textarea>
                </div>
                <div class="input-row"></div>
              </div>
            </div>

            <div class="dialog-content-bottom">
              <div class="input-row">
                <div class="ip-info-2">
                  <div class="b-input input-phone">
                    <div class="label">Số điện thoại</div>
                    <input
                      type="text"
                      class="text-phone"
                      v-model="store.phoneNumber"
                    />
                  </div>
                  <div class="b-input input-tax">
                    <div class="label">Mã số thuế</div>
                    <select class="m-input text-tax">
                      <option>{{ store.storeTaxCode }}</option>
                    </select>
                  </div>
                </div>
              </div>
              <div class="input-row">
                <div class="ip-info-2">
                  <div class="b-input input-country">
                    <div class="label">Quốc gia</div>
                    <select
                      class="m-input select-country"
                      v-model="selectedCountry"
                    >
                      <option
                        v-for="option in optionCountry"
                        :key="option.value"
                        v-bind:value="option.value"
                      >
                        {{ option.text }}
                      </option>
                    </select>
                  </div>
                </div>
              </div>
              <div class="input-row">
                <div class="ip-info-2">
                  <div class="b-input input-province">
                    <div class="label">Tỉnh/Thành phố</div>
                    <select
                      class="m-input select-province"
                      v-model="selectedCity"
                    >
                      <option
                        :value="city.value"
                        v-for="city in optionCity"
                        :key="city.value"
                      >
                        {{ city.text }}
                      </option>
                    </select>
                  </div>
                  <div class="b-input input-distric">
                    <div class="label">Quận/Huyện</div>
                    <select
                      class="m-input select-distric"
                      v-model="selectedDistrict"
                    >
                      <option
                        :value="district.value"
                        v-for="district in optionDistrict"
                        :key="district.value"
                      >
                        {{ district.text }}
                      </option>
                    </select>
                  </div>
                </div>
              </div>
              <div class="input-row">
                <div class="ip-info-2">
                  <div class="b-input input-village">
                    <div class="label">Phường/Xã</div>
                    <select class="m-input select-village" v-model="selectedWard" >
                      <option
                        :value="ward.value"
                        v-for="ward in optionWard"
                        :key="ward.value"
                      >
                        {{ ward.text }}
                      </option>
                    </select>
                  </div>
                  <div class="b-input input-street">
                    <div class="label">Đường phố</div>
                    <select class="m-input text-street"></select>
                  </div>
                </div>
              </div>
            </div>
          </form>
        </div>
        <div class="dialog-footer">
          <div class="leftchild">
            <div class="d-button dbtn-support">
              <div class="icon"></div>
              <div class="text-support">Trợ giúp</div>
            </div>
          </div>
          <div class="rightchild">
            <div class="d-button dbtn-save">
              <div class="icon"></div>
              <div class="text-support">Lưu</div>
            </div>
            <div class="d-button dbtn-get">
              <div class="icon"></div>
              <div class="text-support">Lưu và thêm mới</div>
            </div>
            <div class="d-button dbtn-cancle" @click="hide">
              <div class="icon"></div>
              <div class="text-support">Hủy bỏ</div>
            </div>
          </div>
        </div>
      </BaseModal>
    </div>
  </div>
</template>

<script>
import BaseModal from "../BaseModalForm.vue";
import axios from "axios";

export default {
  components: {
    BaseModal,
  },
  props: {
    store: Object,
  },

  methods: {
    // hiện dialog thêm
    async showAddDialog() {
      this.$refs.BaseModal_ref.show();
      await this.getCounTryData();
      this.selectedCountry = 0;
    },

    // hiện dialog sửa
    showEditDialog: async function () {
      this.$refs.BaseModal_ref.show();
      this.optionDistrict = [];
      this.optionCity = [];
      this.optionWard = [];
      await this.getCounTryData();
      await (this.selectedCountry = this.store.countryId);
      await this.getProvince();
      await (this.selectedCity = this.store.provinceId);
      await this.getDistrict();
      await (this.selectedDistrict = this.store.districtId);
      await this.getWard();
      this.selectedWard = this.store.wardId
    },

    // ẩn dialog
    hide() {
      this.$refs.BaseModal_ref.hide();
    },

    //lấy danh sách quốc gia
    getCounTryData: async function () {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Countrys"
      );
      var optionCountry = [];
      optionCountry.push({ text: "--quốc gia--", value: 0 });
      response.data.data.forEach(function (item) {
        optionCountry.push({
          text: item.countryName,
          value: item.countryId,
        });
      });
      this.optionCountry = optionCountry;
    },

    // lấy danh sách tỉnh theo quốc gia
    getProvince: async function () {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Provinces/WithCountry/" +
          this.selectedCountry
      );

      var optionCity = [];
      optionCity.push({ text: "--Tỉnh/Thành phố--", value: 0 });
      response.data.data.forEach(function (item) {
        optionCity.push({
          text: item.provinceName,
          value: item.provinceId,
        });
      });
      this.optionCity = optionCity;
    },

    //lấy danh sách huyện theo tỉnh
    getDistrict: async function () {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Districts/WithProvince/" +
          this.selectedCity
      );

      var optionDistrict = [];
      optionDistrict.push({ text: "--Huyện/Quận--", value: 0 });
      response.data.data.forEach(function (item) {
        optionDistrict.push({
          text: item.districtName,
          value: item.districtId,
        });
      });
      this.optionDistrict = optionDistrict;
    },

    //lấy danh sách phường xã theo huyện
    getWard: async function () {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Wards/WithDistrict/" +
          this.selectedDistrict
      );

      var optionWard = [];
      optionWard.push({ text: "--Phường/Xã--", value: 0 });
      response.data.data.forEach(function (item) {
        optionWard.push({
          text: item.wardName,
          value: item.wardId,
        });
      });
      this.optionWard = optionWard;
    },
  },
  data() {
    return {
      selectedCountry: 0,

      optionCountry: [{ text: "--quốc gia--", value: 0 }],
      selectedCity: 0,
      optionCity: [{ text: "--tỉnh/thành phố--", value: 0 }],
      selectedDistrict: 0,
      optionDistrict: [{ text: "--quận/huyện--", value: 0 }],
      optionWard: [{ text: "--xã/phường--", value: 0 }],
      selectedWard:0
    };
  },

  watch: {
    selectedCountry: async function () {
      await this.getProvince();
      this.selectedCity = 0;
    },
    selectedCity: async function () {
      await this.getDistrict();
      this.selectedDistrict = 0;
    },
    selectedDistrict: async function () {
      await this.getWard();
    },
  },
};
</script>

<style scoped>
.dialog-Customer {
  z-index: 1000;
  width: 596px;
  height: 491px;
  border-radius: 5px;
  position: absolute;
  top: calc(50% - 300px);
  left: calc(50% - 350px);
  border: 2px solid #e5e6e5;
}

.dialog-Customer .header-dialog {
  height: 20px;
  padding: 10px 14px;
  display: flex;
  align-items: center;
  position: relative;
}

.dialog-Customer .body-dialog {
  padding: 16px 16px 10px 16px;
  margin-bottom: 14px;
  border-bottom: 1px solid #d0d0d0;
  width: a;
  height: auto;
}

.dialog-Customer .body-dialog form {
  width: 564px;
}

.dialog-Customer .body-dialog form .dialog-content-top {
  width: 100%;
  /* display: flex; */
}

.dialog-Customer .body-dialog form .info-avatar .Customer-avatar {
  width: 190px;
  height: 190px;
  border: 2px solid #e5e5e5;
  border-radius: 50%;

  /* background-image: url('../../assets/img/default-avatar.jpg'); */
  background-repeat: no-repeat;
  background-size: contain;
  margin: auto;
}

.dialog-Customer .body-dialog form .info-avatar text-help {
  width: calc(100% / 3);
  height: auto;
  text-align: center;
}

.dialog-Customer .body-dialog form .input-top {
  width: calc(200% / 3);
  height: auto;
  margin-left: 16px;
}

.dialog-Customer .body-dialog form .input-top .input-row {
  display: flex;
  width: 100%;
  margin-bottom: 16px;
}

.input-row .ip-info-1:first-child {
  margin-right: 16px;
  display: flex;
}

.ip-info-1 {
  width: 100%;
  position: relative;
}

.input-row .label {
  font-size: 13px;
  color: #000000;
  /* margin-bottom: 6px; */
  font-weight: 500;
  min-width: 100px;
  padding: 8px 5px 8px 0;
  text-align: left;
  display: flex;
  align-items: center;
}

.ip-info-1 input[type="text"] {
  /* border: 1px solid; */
  outline: none;
  min-width: 453px;
  margin-top: 10px;
  padding: 0;
  height: 33px !important;
}

.ip-info-1 input[type="text"]:focus {
  border: 1px solid #636dde;
}

.ip-info-1 .gender-select {
  width: 30%;
  display: flex;
  align-items: center;
  justify-content: left;
}

.ip-info-1 .gender-box {
  display: flex;
  align-items: center;
  margin-left: -5px;
}

.dialog-content .dialog-content-bottom {
  width: 100%;
  height: 50%;
}

.ip-left {
  width: calc(100% - 186px);
  margin-right: 16px;
}

.ip-left input,
.ip-right input,
.input-address input {
  width: 100%;
}

.ip-right {
  width: 175px;
  position: absolute;
  right: 24px;
}

.input-row {
  display: flex;
  width: 100%;
}

.input-address {
  width: 100%;
  display: block;
}

.dialog-layout {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: #000000;
  opacity: 0.5;
  z-index: 999;
}

.dialog-footer {
  height: 35px;
}

.dialog-footer-btn {
  height: 60px;
  position: absolute;
  right: 24px;
  display: flex;
  align-items: center;
}

.dialog-footer .btn-cancel {
  background-color: #e5e5e5;
  margin-right: 24px;
}

.dialog-footer .btn-cancel,
.btn-save {
  width: 100px;
  height: 40px;
  font-size: 13px;
  border-radius: 4px;
  padding: 0;
  cursor: pointer;
  background-color: #e5e5e5;
}

.dialog-footer .btn-cancel:hover {
  background-color: grey;
}

.m-btn {
  border: none;
  outline: none;
}

.btn-icon {
  width: 16px;
  height: 16px;
  margin: auto 8px auto 16px;
}

.dialog-footer .btn-save {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #ffffff;
  background-color: #019160;
}

.dialog-footer .btn-save-text {
  margin-right: 16px;
}

tbody tr:nth-child(even) {
  background: #f6f6f6;
}

tbody tr:hover {
  background-color: #e5e5e5;
  cursor: pointer;
}

.paging-container .btn-move-page {
  border-radius: 4px;
}

.paging-container .p-number,
.paging-container .btn-move-page {
  height: 34px;
  width: 34px;
  margin: 0 8px 0 8px;
  text-align: center;
  background-repeat: no-repeat;
  background-size: contain;
  background-size: 24px;
  background-position: center;
}

.paging-container .p-number:hover,
.paging-container .btn-move-page:hover {
  background-color: #bbbbbb;
  cursor: pointer;
}

.paging-container .p-number {
  border-radius: 50%;
  border: 1px solid #bbbbbb;
  line-height: 34px;
}

.paging-container .btn-first-page {
  /* background-image: url('../../assets/icon/btn-firstpage.svg'); */
}

.prev-page {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -700px -124px; */
}

.paging-container .isActive {
  background-color: #019160;
}

.right-content .remote-container {
  height: 36px;
  background-color: #2b3173;
  display: flex;
  align-items: center;
}

.right-content .right-content-grid {
  border: 1px solid #e5e6ff;
  background-color: #e5e6eb;
}

.right-content .right-content-grid .r-button {
  color: white;
  /* display: inline; */
  width: -webkit-fit-content;
  width: -moz-fit-content;
  width: fit-content;
  display: flex;
  padding: auto;
  padding: 0 12px 0 0px;
}

.x-btn-text.x-btn-icon-left > .x-btn-icon-el-default-toolbar-small {
  margin-right: 3px;
}

.x-btn-icon-left > .x-btn-icon-el-default-toolbar-small,
.x-btn-icon-right > .x-btn-icon-el-default-toolbar-small {
  width: 16px;
}

.icon-btnnew-white {
  background: url(/QLCH/resources/images/common-icon.png) no-repeat -1px -127px;
}

.x-btn-icon-el-default-toolbar-small {
  font-size: 16px;
  height: 16px;
  color: #919191;
  line-height: 16px;
}

.x-btn-icon {
  height: 16px;
  width: 16px;
  margin-right: 8px;
  margin-left: 7px;
}

.icon-btnclone {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -976px -127px; */
}

.icon-insert {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -1px -127px; */
}

.icon-update {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -77px -203px; */
}

.icon-delete {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -1076px -127px; */
}

.icon-refresh {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -876px -127px; */
}

.button-remote:hover {
  background: #6b6f9d;
  cursor: pointer;
}

.button-remote {
  height: 100%;
  display: flex;
  align-items: center;
  margin-left: 1px;
  border-left: 1px solid #190472;
}

.remote-container .button-addCustomer {
  border-left: 0px !important;
}

.x-panel {
  /* height: 100%;
    width: 100%;
    background: #e5e6eb; */
  height: calc(100% - 36px);
  position: relative;
}

.x-panel .x-grid-header {
  /* height: 64px;
    border-top: 1px solid #e1e1e1!important;
    border-left: 1px solid #e1e1e1!important;
    background: #f0f0f0!important; */
  height: 64px;
  background: #f0f0f0 !important;
  color: #212121;
}

.x-panel .x-grid-body {
  height: calc(100% - 119px);
  border-top: 1px solid #e1e1e1;
  border-bottom: 1px solid #e1e1e1;
  background: #ffffff;
  color: #404040;
}

.x-panel .x-grid-footer {
  height: 32px;
  border-bottom: 1px solid #e1e1e1 !important;
  border-left: 1px solid #e1e1e1 !important;
  border-right: 1px solid #e1e1e1 !important;
  padding: 10px;
  background-color: #fff;
  margin: 0 -1px;
}

.x-panel .x-grid-footer .paging-toolbar {
  height: 100%;
  display: flex;
}

.x-panel .x-grid-footer .paging-toolbar .leftchild {
  height: 100%;
  min-width: 330px;
  display: flex;
  align-items: center;
}

.x-panel .x-grid-footer .paging-toolbar .leftchild .p-button {
  height: 24px;
  width: 24px;
  border: 1px solid #d0d0d0;
  border-radius: 3px;
  background-color: #fff;
  margin-right: 2px;
}

.right-content-grid {
  height: calc(100% - 80px);
  background-color: rebeccapurple;
}

.right-content-grid {
  height: 100%;
  background-color: rebecapurple !important;
}

.x-grid-header {
  display: flex;
}

.x-grid-header .x-column-header {
  height: 100%;
  border-right: 1px solid #d0d0d0;
}

.x-grid-header .x-column-header .x-column-header-inner {
  height: 19px;
  padding: 7px 10px 6px 10px;
  font-weight: 700px;
}

.x-column-header-condition {
  height: 32px;
  border-bottom: 1px solid #d0d0d0;
  border-right: 1px solid #d0d0d0;
  margin-right: -1px;
  display: flex;
  background-color: #fff;
}

.condition-btn {
  min-width: 31px !important;
  border: 1px solid #d0d0d0;
  border-bottom: none;
  margin-left: 1px;
}

.condition-text {
  width: 100%;
  height: 31px;
  border: 1px solid #d0d0d0;
  margin-right: 2px;
  margin-bottom: 1px;
}

.x-grid-header .column-storeid {
  min-width: 159px;
}

.x-grid-header .column-storename {
  min-width: 249px;
}

.x-grid-header .column-storeaddress {
  min-width: 508px !important;
}

.x-grid-header .column-storenumber {
  min-width: 129px;
}

.x-grid-header .column-storestatus {
  min-width: calc(100% - 1050px);
}

/* 
table .th-storeid{
    min-width: 160px;
}
table .th-storename{
    min-width: 250px; 
} */

.x-column-header-inner .x-fontw {
  font-weight: 700;
}

/* table tr td:nth-child(1){
    min-width: 159px;
}

table tr td:nth-child(2){
    min-width: 249px;
}
table tr td:nth-child(3){
    min-width: 491px;
}
table tr td:nth-child(4){
    min-width: 129px;
}
table tr td:nth-child(5){
    min-width: calc(100% - 1033px);
} */

table {
  width: 100%;
}

table td {
  padding: 7px 10px 6px 10px;
  text-align: left;
  height: 19px;
  border-right: 1px solid #e9e9e9;
  border-bottom: 1px solid #e9e9e9;
}

table thead tr :nth-child(1) {
  min-width: 159px;
  width: 160px !important;
}

table thead tr :nth-child(2) {
  min-width: 249px;
  width: 250px !important;
}

table thead tr :nth-child(3) {
  min-width: 508px;
  width: 492px !important;
}

table thead tr :nth-child(4) {
  min-width: 129px;
  width: 130px !important;
}

.select-quantitypage {
  width: 46px;
  height: 26px;
  border: 1px solid #d0d0d0;
  outline: none !important;
}

.text-pagebumber {
  width: 36px;
  height: 16px;
  padding: 4px 6px;
  border: 1px solid #d0d0d0;
}

.text-pagebumber,
.select-quantitypage {
  border-radius: 3px;
  text-align: center;
}

.select-quantitypage {
  appearance: none;
  /* background: url(../../assets/icon/arrow-down-line.png) no-repeat; */
  background-position: 29px 11px;
  padding-left: 4px;
}

.x-panel .x-grid-footer .paging-toolbar .leftchild .first-page {
  /* background: url(/QLCH/resources/images/common-icon.png) no-repeat -649px -124px;
    background: url(../../assets/icon/common-icon.png) no-repeat;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center; */
  /* background: url(../../assets/icon/common-icon.png) no-repeat -649px -124px; */
  width: 24px;
  height: 24px;
  background-color: #fff;
  border-radius: 3px;
  cursor: pointer;
}

.refresh {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -849px -124px; */
  border: 1px solid #6b6f9d !important;
}

.leftchild .last-page {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -798px -124px; */
}

.leftchild .next-page {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -749px -124px; */
}

.x-grid-footer {
  display: flex;
}

.rightchild {
  position: absolute;
  right: 0px;
  height: 32px;
  display: flex;
  align-items: center;
}

.dialog-content-bottom .ip-info-2 {
  height: 35px;
  margin-top: 10px;
  width: 100%;
  display: flex;
}

.ip-info-2 .b-input {
  display: flex;
  align-items: center;
}

.ip-info-2 .m-input {
  min-width: 167px;
  height: 35px !important;
}

.input-tax,
.input-district,
.input-street {
  margin-right: 0;
}

.ip-info-1 input[type="text"] {
  border: 1px solid #d0d0d0;
}

.ip-info-2 .m-input {
  min-width: 167px !important;
  height: 35px !important;
  border: 1px solid #d0d0d0;
  border-radius: 4px;
}

.dialog-content-bottom .text-phone {
  min-width: 161px !important;
  height: 33px !important;
  border: 1px solid #d0d0d0;
  border-radius: 4px;
  padding: 0;
}

.input-tax .label,
.input-distric .label,
.input-street .label {
  text-align: center;
  padding: 8px 0 8px 25px;
}

.text-phone {
  width: 167px;
  height: 35px;
}

.input-phone {
  width: 272px !important;
  height: 35px !important;
}

.dialog-footer {
  display: flex;
  align-items: center;
  position: relative;
  margin: 0 8px;
}

.dialog-footer .leftchild {
  height: 100%;
  width: 96px;
}

.dialog-footer .rightchild {
  height: 100%;
}

.dialog-footer .rightchild .dbtn-save {
  width: 65px;
}

.dialog-footer .rightchild .dbtn-get {
  width: 124px;
  margin-right: 10px;
  border: 1px solid #2b3173;
}

.dialog-footer .rightchild .dbtn-cancle {
  width: 74px;
  border: 1px solid white;
}

.dialog-footer .d-button {
  height: calc(100% - 2px);
  border-radius: 4px;
  display: flex;
  align-items: center;
  padding: 0 7px;
}

/* .dialog-footer  .icon{
    height: 16px;
    width: 16px;
    background-position: center!important;
    background-size: 12px!important;
    margin-right: 3px;
} */

.dialog-footer .dbtn-support .icon {
  /* background: url(../../assets/icon/icon_help_18.png) no-repeat 4px 1px; */
  background-repeat: no-repeat;
  height: 16px;
  width: 16px;
  background-position: center !important;
  background-size: 12px !important;
  margin-right: 6px;
}

.dialog-footer .dbtn-save .icon {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -327px -127px;
    background: url(../../assets/img/common-icon.6cf6ba71.png) no-repeat -327px -127px; */
  height: 16px;
  width: 16px;
  margin-right: 6px;
}

.dialog-footer .dbtn-get .icon {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -26px -127px; */
  background-repeat: no-repeat;
  height: 16px;
  width: 16px;
  /* background-position: center!important; */
  /* background-size: contain!important; */
  margin-right: 6px;
}

.dialog-footer .dbtn-cancle .icon {
  /* background: url(../../assets/icon/common-icon.png) no-repeat -252px -127px; */
  background-repeat: no-repeat;
  height: 16px;
  width: 16px;
}

.dialog-footer .dbtn-save {
  background-color: #2b3173;
  color: white;
  border: 1px solid #2b3173;
  margin-right: 10px;
}

.dialog-footer {
  color: #2b3173;
  font-weight: 600;
  font-size: 12px;
}

.dialog-Customer {
  background-color: #fff;
}

.header-dialog {
  background-color: #dfdfdf;
}

.header-dialog .header-title {
  font: 700 16px roboto !important;
  color: #212121;
  float: left;
}

.header-dialog .btn-close {
  height: 16px;
  width: 16px;
  position: absolute;
  right: 14px;
  /* background: url(../../assets/img/common-icon.6cf6ba71.png) no-repeat -1102px -153px; */
  /* color: #fff; */
  opacity: 0.8;
  border: none;
}

.dialog-footer .d-button:hover {
  border: 1px solid #2b3173 !important;
  cursor: pointer;
}

.ip-info-1 .area-address {
  min-height: 80px;
  width: 100%;
  border: 1px solid #d0d0d0;
  min-width: 457px;
  margin-top: 10px;
  border-radius: 4px;
  outline: none;
  padding: 0;
}

.ip-info-1 .area-address:focus {
  border: 1px solid #636dde;
}

.header-dialog .btn-close:hover {
  cursor: pointer;
}

.dialog-Customer input,
.dialog-Customer select {
  outline: none;
}

.dialog-Customer input:focus,
.dialog-Customer select:focus {
  border: 1px solid #636dde;
}

.dialog-footer .dbtn-save:hover {
  background-color: #6b6f9d;
}

.dialog-footer .rightchild .dbtn-get:hover {
  color: #6b6f9d;
}

.dialog-footer .leftchild .dbtn-support:hover {
  background: #e5e6eb;
  border: none !important;
}

.boderRed {
  border: 1px solid red !important;
  min-width: 431px !important;
}

.dialog-content .lb-address {
  margin-top: 10px;
  align-items: flex-start;
}

.label span {
  color: red;
}

.x-grid-table {
  width: 100%;
  /* background-color: rebeccapurple; */
  height: calc(100% - 36px);
  overflow: scroll;
}
</style>