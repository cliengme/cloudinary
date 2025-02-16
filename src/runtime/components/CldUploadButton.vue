<script setup lang="ts">
export interface CldUploadWidgetPropsOptions {
  // Widget

  encryption?: {
    key: string;
    iv: string;
  };
  defaultSource?: string;
  maxFiles?: number;
  multiple?: boolean;
  sources?: Array<
    | "camera"
    | "dropbox"
    | "facebook"
    | "gettyimages"
    | "google_drive"
    | "image_search"
    | "instagram"
    | "istock"
    | "local"
    | "shutterstock"
    | "unsplash"
    | "url"
  >;

  // Cropping

  cropping?: boolean;
  croppingAspectRatio?: number;
  croppingCoordinatesMode?: string;
  croppingDefaultSelectionRatio?: number;
  croppingShowBackButton?: boolean;
  croppingShowDimensions?: boolean;
  showSkipCropButton?: boolean;

  // Sources

  dropboxAppKey?: string;
  facebookAppId?: string;
  googleApiKey?: string;
  googleDriveClientId?: string;
  instagramClientId?: string;
  searchByRights?: boolean;
  searchBySites?: Array<string>;

  // Upload

  context?: object;
  folder?: string;
  publicId?: string;
  resourceType?: string;
  tags?: Array<string>;
  uploadSignature?: string | Function;
  uploadSignatureTimestamp?: number;

  // Client Side

  clientAllowedFormats?: Array<string>;
  croppingValidateDimensions?: boolean;
  maxChunkSize?: number;
  maxImageFileSize?: number;
  maxImageHeight?: number;
  maxImageWidth?: number;
  maxFileSize?: number;
  maxRawFileSize?: number;
  maxVideoFileSize?: number;
  minImageHeight?: number;
  minImageWidth?: number;
  validateMaxWidthHeight?: boolean;

  // Containing Page

  fieldName?: string;
  form?: string;
  thumbnails?: string;
  thumbnailTransformation?: string | Array<object>;

  // Customization

  buttonCaption?: string;
  buttonClass?: string;
  text?: object;
  theme?: string;
  styles?: object;

  // Advanced

  autoMinimize?: boolean;
  getTags?: Function;
  getUploadPresets?: Function;
  inlineContainer?: any; // string or DOM element
  language?: string;
  preBatch?: Function;
  prepareUploadParams?: Function;
  queueViewPosition?: string;
  showAdvancedOptions?: boolean;
  showCompletedButton?: boolean;
  showInsecurePreview?: boolean;
  showPoweredBy?: boolean;
  showUploadMoreButton?: boolean;
  singleUploadAutoClose?: boolean;
}

export interface CldUploadWidgetProps {
  onClose?: Function;
  onError?: Function;
  onOpen?: Function;
  onUpload?: Function;
  onClick?: Function;
  onAbort?: Function;
  onBatchCancelled?: Function;
  onDisplayChanged?: Function;
  onPublicId?: Function;
  onQueuesEnd?: Function;
  onQueuesStart?: Function;
  onRetry?: Function;
  onShowCompleted?: Function;
  onSourceChanged?: Function;
  onSuccess?: Function;
  onTags?: Function;
  onUploadAdded?: Function;
  options?: CldUploadWidgetPropsOptions;
  signatureEndpoint?: URL | RequestInfo;
  uploadPreset?: string;
}

defineProps<CldUploadWidgetProps>();
</script>

<template>
  <CldUploadWidget v-slot="{ open, isLoading }" :upload-preset="uploadPreset">
    <button
      type="button"
      v-bind="$attrs"
      :disabled="isLoading"
      @click="(e: Event) => {
        e.preventDefault();
        open();
        if (typeof onClick === 'function') onClick(e)
      }"
    >
      <slot />
    </button>
  </CldUploadWidget>
</template>
