  FROM ibisba/knime-base:3.7.2
  
  RUN "$KNIME_DIR/knime" -application org.eclipse.equinox.p2.director \
  -r "http://update.knime.com/analytics-platform/3.7,https://abibuilder.informatik.uni-tuebingen.de/archive/openms/knime-plugin/updateSite/nightly/" \
  -p2.arch x86_64 \
  -profileProperties org.eclipse.update.install.features=true \
  -i "de.openms.feature.feature.group,com.genericworkflownodes.knime.feature.feature.group" \
  -p KNIMEProfile \
  -nosplash
  
  RUN "$KNIME_DIR/knime" -application org.eclipse.equinox.p2.director \
  -r "http://update.knime.com/analytics-platform/3.7,http://update.knime.com/community-contributions/trunk" \
  -p2.arch x86_64 \
  -profileProperties org.eclipse.update.install.features=true \
  -i "org.knime.features.r.feature.group,org.knime.features.chem.types.feature.group,org.rdkit.knime.feature.feature.group,org.knime.features.ext.svg.feature.group" \
  -p KNIMEProfile \
  -nosplash
