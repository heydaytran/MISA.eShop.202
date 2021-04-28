<template>
  <div>
    <BaseModal ref="BaseModal_ref">
      <div class="dialog-Customer">
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
                  v-if="!store.storeCode"
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
                    <select
                      class="m-input text-tax"
                      v-model="store.storeTaxCode"
                    >
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
                        v-for="(city, index) in optionCity"
                        :key="index"
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
            <div class="d-button dbtn-save" @click="save('addOne')">
              <div class="icon"></div>
              <div class="text-support">Lưu</div>
            </div>
            <div class="d-button dbtn-get" @click="save('addMore')">
              <div class="icon"></div>
              <div class="text-support">Lưu và thêm mới</div>
            </div>
            <div class="d-button dbtn-cancle" @click="hide">
              <div class="icon"></div>
              <div class="text-support">Hủy bỏ</div>
            </div>
          </div>
        </div>
      </div>
    </BaseModal>
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
  props: ["store","formMode"],


  methods: {
    // reset lại input trong modal
    resetInput() {
      this.selectedCountry = null;

      this.optionDistrict = [];
      this.optionDistrict.push({ text: "--Huyện--", value: null });

      this.optionCity = [];
      this.optionCity.push({ text: "--Thành Phố--", value: null });

      this.optionWard = [];
      this.optionWard.push({ text: "--Xã--", value: null });

      (this.store.storeCode = ""),
        (this.store.storeName = ""),
        (this.store.address = ""),
        (this.store.phoneNumber = ""),
        (this.store.storeTaxCode = ""),
        (this.selectedCountry = null),
        (this.selectedDistrict = null),
        (this.selectedWard = null),
        (this.selectedCity = null);
    },

    // hiện dialog thêm
    showAddDialog() {
      this.$refs.BaseModal_ref.show();
      this.resetInput();
      setTimeout(() => {
        document.getElementById("CustomerCode").focus();
      }, 0);
      this.getCounTryData();
      this.formTitle = "Thêm mới cửa hàng";
    },

    // hiện dialog sửa
    showEditDialog: async function (value) {
      this.formTitle = "Chỉnh sửa cửa hàng";
      // debugger; // eslint-disable-line
      // this.$refs.BaseModal_ref.show();
      var res = this;
      
      // console.log(res.selectedCity, "a");
      res.getCounTryData();
      res.selectedCountry = value.countryId;
      
      setTimeout(() => {
      res.selectedCity = res.store.provinceId
        
      }, 1000);
      //res.getProvince(value.provinceId);
      //console.log( res.selectedCity,"city");


      //  await this.getProvince()
      //  .then( res.selectedCity = res.store.provinceId)
      //  .then(this.$refs.BaseModal_ref.show())

      // if (this.selectedCountry != null) {
      //   await this.getProvince();
      //   res.selectedCity = res.store.provinceId;
      //   if (this.selectedCity != null) {
      //     await this.getDistrict();
      //     res.selectedDistrict = res.store.districtId;
      //     if (this.selectedDistrict != null) {
      //       await this.getWard();
      //       res.selectedWard = res.store.wardId;
      //     }
      //   }
      // }
      setTimeout(() => {
        this.$refs.BaseModal_ref.show();
        // console.log(res.selectedCity);
      }, 0);
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
      optionCountry.push({ text: "--quốc gia--", value: null });
      response.data.data.forEach(function (item) {
        optionCountry.push({
          text: item.countryName,
          value: item.countryId,
        });
      });
      this.optionCountry = optionCountry;
    },

    // lấy danh sách tỉnh theo quốc gia
    getProvince: async function (value) {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Provinces/WithCountry/" +
          this.selectedCountry
      );
       console.log(response,"city2");

      var optionCity = [];
      optionCity.push({ text: "--Tỉnh/Thành phố--", value: null });
      response.data.data.forEach(function (item) {
        optionCity.push({
          text: item.provinceName,
          value: item.provinceId,
        });
      });
      this.optionCity = optionCity;
      this.selectedCity = value;
      console.log(value);
    },

    //lấy danh sách huyện theo tỉnh
    getDistrict: async function () {
      const response = await axios.get(
        "http://localhost:35480/api/v1/Districts/WithProvince/" +
          this.selectedCity
      );

      var optionDistrict = [];
      optionDistrict.push({ text: "--Huyện/Quận--", value: null });
      console.log(optionDistrict);
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
      optionWard.push({ text: "--Phường/Xã--", value: null });
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
        //res.parentElement.nextSibling.classList.add("hidden");
        //this.$refs.ModalValidata_ref.hide()
      }
    },

    // lưu bản ghi
    // text = addMore -> lưu và thêm mới
    // text = addOne -> lưu
    async save(text) {
      console.log(text);
      var a;
      a = await this.validateForm();
      var res = this;
      console.log(res.formMode);
      switch (res.formMode) {
        case "add": {
          console.log(a);
          if (a == false) {
            alert("Vui lòng kiểm tra lại các trường đã nhập");
          } else {
            console.log("thêm đối tượng sau: " + res.store);

            res.store.countryId = res.selectedCountry;
            res.store.provinceId = res.selectedCity;
            res.store.districtId = res.selectedDistrict;
            res.store.wardId = res.selectedWard;

            await axios
              .post("http://localhost:35480/api/v1/stores/", res.store)
              .then((respone) => {
                if (text == "addOne") {
                  alert(respone.data.userMsg);
                  if (respone.data.errorCode != 400) {
                    res.hide();
                  }
                } else {
                  res.showAddDialog();
                }
              })
              .catch((err) => {
                console.log(err.response.data);
                alert("Thêm mới thất bại");
              });
          }
          break;
        }
        case "edit": {
          alert("chưa thực hiện");
        }
      }
    },

    // validate toàn bộ form khi lưu
    validateForm() {
      //var res = this;
      var requiredInput = document.getElementsByClassName("required");
      var validStoreCode = true;

      for (let i = 0; i < requiredInput.length; i++) {
        if (requiredInput[i]._value === "") {
          requiredInput[i].classList.add("boderRed");
          requiredInput[i].parentElement.nextSibling.classList.remove("hidden");
          validStoreCode = false;
        }
      }
      return validStoreCode;

      // nếu các trường bắt buộc nhập không trống -> check trùng mã
      // if (
      //   requiredInput[0]._value != "" &&
      //   requiredInput[1]._value != "" &&
      //   requiredInput[2]._value != ""
      // ) {
      //   res.validStoreCode = res.checkDuplicateCode(requiredInput[0]._value);
      //   if (res.validStoreCode === false) {
      //     requiredInput[0].classList.add("boderRed");
      //     requiredInput[0].parentElement.nextSibling.classList.remove("hidden");
      //   }
      //   return validStoreCode;
      // } else return true;
    },

    // check trùng mã
    async checkDuplicateCode(storeCode) {
      var res = this;

      await axios
        .get("http://localhost:35480/api/v1/stores/getbycode", {
          params: {
            storeCode: storeCode,
          },
        })
        .then((respone) => {
          if (respone.data.errorCode == 400) {
            if (res.formMode == "edit") {
              if (respone.data.data.storeId != res.store.storeId) {
                return false;
              } else {
                return true;
              }
            } else {
              alert("mã cửa hàng đã tồn tại");
              return false;
            }
          } else {
            alert("thêm thành công");
            return true;
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  computed: {},

  data() {
    return {
      selectedCountry: null,
      optionCountry: [{ text: "--quốc gia--", value: null }],
      selectedCity: null,
      optionCity: [{ text: "--tỉnh/thành phố--", value: null }],
      selectedDistrict: null,
      optionDistrict: [{ text: "--quận/huyện--", value: null }],
      optionWard: [{ text: "--xã/phường--", value: null }],
      selectedWard: null,
      formTitle: "Thêm mới cửa hàng",
      storeCodeValidate: "",
    };
  },

  watch: {
    selectedCountry: async function () {
      await this.getProvince();
      //this.selectedCity = null;
    },
    selectedCity: async function () {
      await this.getDistrict();
      this.selectedDistrict = null;
    },
    selectedDistrict: async function () {
      await this.getWard();
      this.selectedWard = null;
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