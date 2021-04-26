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


<style src="../../../style/common/_ShopModalCreate.scss" lang="scss" />
