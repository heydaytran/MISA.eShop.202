<template>
  <div>
    <div class="hello">
      <BaseModal ref="BaseModal_ref">
        <div class="header-dialog">
          <div class="header-title">{{ formTitle }}</div>
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
                    class="m-input required"
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
                <ModalEmtyWarning
                  ref="ModalEmtyWarning_ref"
                  v-show="!store.storeCode"
                  class="hidden"
                  :storeCodeValidate="storeCodeValidate"
                />
              </div>
              <div class="input-row">
                <div class="ip-info-1">
                  <div class="label">Tên cửa hàng <span>*</span></div>
                  <input
                    type="text"
                    id="CustomerName"
                    fieldName="FullName"
                    name="Customer-name"
                    class="m-input required"
                    ref="input_2"
                    v-model="store.storeName"
                    @blur="ValidateEmty('input_2')"
                    @keyup="ValidateEmty('input_2')"
                  />
                </div>
                <ModalEmtyWarning v-if="!store.storeName" class="hidden" />
                <div class="input-row"></div>
              </div>
              <div class="input-row">
                <div class="ip-info-1">
                  <div class="label lb-address">Địa chỉ <span>*</span></div>
                  <textarea
                    class="area-address required"
                    aria-hidden="false"
                    aria-disabled="false"
                    aria-multiline="true"
                    role="textbox"
                    v-model="store.address"
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
                <ModalEmtyWarning v-if="!store.address" class="hidden" />
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
                    <select
                      class="m-input select-village"
                      v-model="selectedWard"
                    >
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
            <div class="d-button dbtn-save" @click="validateForm">
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
import ModalEmtyWarning from "../ModalEmtyWarning.vue";

export default {
  components: {
    BaseModal,
    ModalEmtyWarning,
  },
  props: {
    store: Object,
    formMode: String,
  },

  methods: {
    // hiện dialog thêm
    showAddDialog() {
      this.$refs.BaseModal_ref.show();
      setTimeout(() => {
        document.getElementById("CustomerCode").focus();
      }, 0);
      this.getCounTryData();
      this.selectedCountry = 0;
      this.formTitle = "Thêm mới cửa hàng";
    },

    // hiện dialog sửa
    showEditDialog: async function () {
      this.$refs.BaseModal_ref.show();
      this.formTitle = "Chỉnh sửa cửa hàng";
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
      this.selectedWard = this.store.wardId;
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
    ValidateEmty(input) {
      var res = this.$refs[input];
      if (res.value == "") {
        res.classList.add("boderRed");
        // var h = document.getElementById("hidden1");
        // h.classList.remove("hidden");
        res.parentElement.nextSibling.classList.remove("hidden");

        // var phanTuCon = document.getElementById("hidden1");
        // phanTuCon.parentNode.removeChild(phanTuCon);
        //  this.$refs.ModalValidata_ref.show()
      } else {
        res.classList.remove("boderRed");
        res.parentElement.nextSibling.classList.add("hidden");
        //this.$refs.ModalValidata_ref.hide()
      }
    },

    validateForm() {
      var res = this;
      var requiredInput = document.getElementsByClassName("required");
      var validStoreCode;
      for (let i = 0; i < requiredInput.length; i++) {
        if (requiredInput[i]._value === "") {
          requiredInput[i].classList.add("boderRed");
          requiredInput[i].parentElement.nextSibling.classList.remove("hidden");
          continue;
        }
      }
      if (
        requiredInput[0]._value != "" &&
        requiredInput[1]._value != "" &&
        requiredInput[2]._value != ""
      ) {
        validStoreCode = res.checkDuplicateCode(requiredInput[0]._value);
        if (validStoreCode === false) {
          requiredInput[0].classList.add("boderRed");
          requiredInput[0].parentElement.nextSibling.classList.remove("hidden");
        }
        return validStoreCode;
      } else return false;
    },

    // check trùng mã
    checkDuplicateCode(storeCode) {
      var res = this;
      axios
        .get("http://localhost:35480/api/v1/stores/getbycode", {
          params: {
            storeCode: storeCode,
          },
        })
        .then((respone) => {
          let valid = true;
          if (respone.data.errorCode == 400) {
            res.$refs.ModalEmtyWarning_ref.warningText =
              "Mã cửa hàng đã bị trùng";
            if (this.formMode == "edit") {
              if (respone.data.data.storeId != this.store.storeId) {
                this.validate.storeCode = false;
                this.warningMsg1 = "Mã cửa hàng đã tồn tại - sửa ";
                this.storeCodeValidate = "Mã cửa hàng đã bị trùng";
                valid = false;
              } else {
                this.validate.storeCode = true;
                valid = true;
              }
            } else {
              alert("mã cửa hàng đã tồn tại");
              this.storeCodeValidate = "Mã cửa hàng đã bị trùng";
              valid = false;
            }
            valid = false;
          } else {
            alert("thêm thành công");
            valid = true;
          }
          return valid;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  computed: {},

  data() {
    return {
      selectedCountry: 0,

      optionCountry: [{ text: "--quốc gia--", value: 0 }],
      selectedCity: 0,
      optionCity: [{ text: "--tỉnh/thành phố--", value: 0 }],
      selectedDistrict: 0,
      optionDistrict: [{ text: "--quận/huyện--", value: 0 }],
      optionWard: [{ text: "--xã/phường--", value: 0 }],
      selectedWard: 0,
      formTitle: "Thêm mới cửa hàng",
      storeCodeValidate: "Trường này không được để trống",
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

<style src="../../../style/common/_ShopModalCreate.scss" lang="scss" />
<style scoped>
.hidden {
  display: none;
}
</style>